# 2b IMPLEMENTATION OF SLIDING WINDOW PROTOCOL
## AIM
## ALGORITHM:
1. Start the program.
2. Get the frame size from the user
3. To create the frame based on the user request.
4. To send frames to server from the client side.
5. If your frames reach the server it will send ACK signal to client
6. Stop the Program
## PROGRAM 
CLIENT:
~~~
import socket
s = socket.socket()
s.bind(('localhost', 9999))
s.listen(1)
print("Server listening...")
conn, addr = s.accept()
print(f"Connected to {addr}")

while True:
    frames = conn.recv(1024).decode()
    if not frames:
        break

    print(f"Received frames: {frames}")
    ack_message = f"ACK for frames: {frames}"
    conn.send(ack_message.encode())

conn.close()  
s.close()  
~~~
server:
~~~
 import socket
c = socket.socket()
c.connect(('localhost', 9999))

size = int(input("Enter number of frames to send: "))
l = list(range(size))  
print("Total frames to send:", len(l))
s = int(input("Enter Window Size: "))

i = 0
while True:
    while i < len(l):
        st = i + s
        frames_to_send = l[i:st]  
        print(f"Sending frames: {frames_to_send}")
        c.send(str(frames_to_send).encode())  

        ack = c.recv(1024).decode()  
        if ack:
            print(f"Acknowledgment received: {ack}")
            i += s  

    break
c.close()
~~~
## OUPUT
client:
<img width="930" height="267" alt="498092252-c3fff252-9fba-4473-b085-25257af139f2 (1)" src="https://github.com/user-attachments/assets/9987dd2d-b475-4838-a2c1-668068377472" />
server:
<img width="935" height="272" alt="498092534-b1055d86-a111-49f5-8931-70e2ac62b261" src="https://github.com/user-attachments/assets/3491f97c-d55d-4cd4-97ed-8f2ec70ff469" />

## RESULT

Thus, python program to perform stop and wait protocol was successfully executed
