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

Developed by : **ARUL KUMARAN S A**

Reg no : **212224040030**

### Client
```python
import socket
s = socket.socket()
s.bind(('localhost',8002))
s.listen(5)
c, addr = s.accept()
ListSize = int(input("Enter the number of frames to send : "))
List = list(range(ListSize))
WindowSize = int(input("Enter Window Size : "))
st, i = 0, 0
while True:
    while(i < ListSize):
        st += WindowSize
        c.send(str(List[i:st]).encode())
        Acknowledgment = c.recv(1024).decode()
        if Acknowledgment:
            print(Acknowledgment)
            i+=st

```

### Server
```python
import socket
s = socket.socket()
s.connect(('localhost', 8002))
while True:
    print(s.recv(1024).decode())
    s.send("Acknowledgement received from the server".encode())
```

## OUPUT
Refer to the screenshot below to see the output of the program

<img width="1832" height="502" alt="image" src="https://github.com/user-attachments/assets/97ab3819-a9c9-4bba-8ad4-fb8436395793" />


## RESULT
Thus, python program to perform stop and wait protocol was successfully executed.
