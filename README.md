# 2b IMPLEMENTATION OF SLIDING WINDOW PROTOCOL
## AIM
To implement a program to illustrate the mechanism of sliding window protocol
## ALGORITHM:
1. Start the program.
2. Get the frame size from the user
3. To create the frame based on the user request.
4. To send frames to server from the client side.
5. If your frames reach the server it will send ACK signal to client
6. Stop the Program
## PROGRAM

### Client
```python
import socket

# Create a socket
s = socket.socket()
s.connect(('localhost', 8000))
print("Connected to the server successfully!")
while True:
    data = s.recv(1024).decode()
    if not data:
        print("No more frames to receive. Closing connection.")
        break

    print(f"Received frames: {data}")
    
    # Send acknowledgment back to the server
    s.send("Acknowledgment received from client.".encode())

s.close()

```

### Server
```python
import socket

# Create a socket
s = socket.socket()
s.bind(('localhost', 8000))
s.listen(5)
print("Server is waiting for connection...")

# Accept connection
c, addr = s.accept()
print("Connected with:", addr)

# Input number of frames
size = int(input("Enter number of frames to send: "))
frames = list(range(size))

# Input window size
window_size = int(input("Enter Window Size: "))

start = 0  # Starting frame index

# Send frames in windows
while start < len(frames):
    end = start + window_size
    window = frames[start:end]
    print(f"Sending frames: {window}")
    
    # Send the current window
    c.send(str(window).encode())
    
    # Wait for acknowledgment
    ack = c.recv(1024).decode()
    if ack:
        print(f"Acknowledgment received for frames up to: {ack}")
        start += window_size  # Move the window

print("All frames sent successfully.")
c.close()
s.close()
```

## OUPUT
Refer to the screenshot below to see the output of the program

<img width="1918" height="1198" alt="image" src="https://github.com/user-attachments/assets/eb9b3497-b5c0-470a-98f3-745f066b464d" />



## RESULT
Thus, python program to perform stop and wait protocol was successfully executed.
