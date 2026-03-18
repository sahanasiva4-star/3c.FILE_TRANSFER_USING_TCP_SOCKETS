# 3c.CREATION FOR FILE TRANSFER USING TCP SOCKETS
## AIM
To write a python program for creating File Transfer using TCP Sockets Links

## ALGORITHM:
1. Import the necessary python modules.
2. Create a socket connection using socket module.
3. Send the message to write into the file to the client file.
4. Open the file and then send it to the client in byte format.
5. In the client side receive the file from server and then write the content into it.
   
## PROGRAM
server.py
~~~
import socket, os

s = socket.socket()
s.bind(('127.0.0.1', 65432))
s.listen(1)

print("Server running...")

while True:
    conn, addr = s.accept()
    print("Connected:", addr)

    file = conn.recv(1024).decode()

    if os.path.isfile(file):
        conn.send(b"OK")
        with open(file, 'rb') as f:
            conn.sendall(f.read())
    else:
        conn.send(b"NO")

    conn.close()
~~~
client.py
~~~
import socket

s = socket.socket()
s.connect(('127.0.0.1', 65432))

file = input("Enter filename: ")
s.send(file.encode())

response = s.recv(1024)

if response == b"OK":
    with open("received_" + file, "wb") as f:
        while True:
            data = s.recv(1024)
            if not data:
                break
            f.write(data)
    print("File received successfully")
else:
    print("File not found")

s.close()
~~~

## OUPUT
<img width="1855" height="199" alt="image" src="https://github.com/user-attachments/assets/07def721-a435-404d-b44e-c9c66e756197" />
<img width="1863" height="286" alt="image" src="https://github.com/user-attachments/assets/6ff4ea0f-48cc-4d39-ba77-aa5f0d7c5086" />

## RESULT
Thus, the python program for creating File Transfer using TCP Sockets Links was 
successfully created and executed.
