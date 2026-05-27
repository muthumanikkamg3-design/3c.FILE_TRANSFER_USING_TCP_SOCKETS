# 3c.CREATION FOR FILE TRANSFER USING TCP SOCKETS

Developed by :MUTHU MANIKKAM.G

Reg No :2122251000229

## AIM
To write a python program for creating File Transfer using TCP Sockets Links
## ALGORITHM:
1. Import the necessary python modules.
2. Create a socket connection using socket module.
3. Send the message to write into the file to the client file.
4. Open the file and then send it to the client in byte format.
5. In the client side receive the file from server and then write the content into it.
## PROGRAM:

Client Code:

client.py

~~~
import socket
s = socket.socket()
host = socket.gethostname()
port = 60000
s.connect((host, port))
s.send("Hello server!".encode())
with open('mytext.txt', 'wb') as f:
 while True:
    print('receiving data...')
    data = s.recv(1024)
    print('data=%s', (data))
    if not data:
        break
    f.write(data)
f.close()
print('Successfully get the file')
s.close()
print('connection closed')
~~~

Server Code:

server.py

~~~
import socket

port = 60000

# Create socket
s = socket.socket()

host = socket.gethostname()

# Bind socket
s.bind((host, port))

# Listen for connection
s.listen(5)

print("Server waiting...")

while True:
    conn, addr = s.accept()

    print("Connected from:", addr)

    data = conn.recv(1024)
    print("Server received", repr(data))

    # File name
    filename = "mytext.txt"

    try:
        f = open(filename, 'rb')

        l = f.read(1024)

        while l:
            conn.send(l)
            print("Sent", repr(l))
            l = f.read(1024)

        f.close()

        print("Done sending")

        conn.send("Thank you for connecting".encode())

    except FileNotFoundError:
        print("File not found")

    conn.close()
~~~


## OUPUT:
<img width="1402" height="328" alt="image" src="https://github.com/user-attachments/assets/5feb4e15-1993-405d-9f7b-3732c602bb1a" />

## RESULT
Thus, the python program for creating File Transfer using TCP Sockets Links was 
successfully created and executed.
