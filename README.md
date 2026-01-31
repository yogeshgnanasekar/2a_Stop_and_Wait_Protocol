# 2a_Stop_and_Wait_Protocol
## AIM 
To write a python program to perform stop and wait protocol
## ALGORITHM
1. Start the program.
2. Get the frame size from the user
3. To create the frame based on the user request.
4. To send frames to server from the client side.
5. If your frames reach the server it will send ACK signal to client
6. Stop the Program
## PROGRAM

## client.py
   import socket
import time

client = socket.socket()
client.connect(('localhost', 8000))
client.settimeout(5)  

while True:
    msg = input("Enter a message (or type 'exit' to quit): ")

    client.send(msg.encode())  

    if msg.lower() == 'exit':  
        print("Connection closed by client")
        client.close()
        break

    try:
        ack = client.recv(1024).decode()
        if ack == "ACK":
            print(f"Server acknowledged: {ack}")
    except socket.timeout:
        print("No ACK received, retransmitting...")
        continue

  ## sever.py
  import socket

server = socket.socket()
server.bind(('localhost', 8000))
server.listen(1)
print("Server is listening...")
conn, addr = server.accept()
print(f"Connected with {addr}")

while True:
    data = conn.recv(1024).decode()

    if data:
        print(f"Received: {data}")
        conn.send("ACK".encode())

        if data.lower() == 'exit':  
            print("Connection closed by client")
            conn.close()
            break
## OUTPUT

<img width="1040" height="300" alt="Screenshot 2026-01-31 135322" src="https://github.com/user-attachments/assets/c86a4b26-b941-4ff5-abd2-e2bc0e1cbd6a" />

<img width="1021" height="207" alt="Screenshot 2026-01-31 135333" src="https://github.com/user-attachments/assets/3e7bbcda-8af2-4f1f-a274-b67658f5f804" />

## RESULT
Thus, python program to perform stop and wait protocol was successfully executed.
