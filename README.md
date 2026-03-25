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
```
import socket

HOST = socket.gethostname()
PORT = 60000
FILE = "mytext.txt"

with socket.socket() as s:
    s.bind((HOST, PORT))
    s.listen(1)
    print("Server listening...")
    while True:
        conn, addr = s.accept()
        print("Connected:", addr)

        msg = conn.recv(1024)    # <-- FIX: read client hello
        print("Client says:", msg.decode())
        FILE='D:\\SEM-2\\CN\\EX-3c\\3c.FILE_TRANSFER_USING_TCP_SOCKETS\\mytext.txt'
        with open(FILE, "rb") as f:
            for chunk in iter(lambda: f.read(1024), b""):
                conn.sendall(chunk)

        conn.shutdown(socket.SHUT_WR)   # tell client sending finished
        conn.close()
        print("File sent & connection closed")
```
```
import socket

HOST = socket.gethostname()
PORT = 60000

with socket.socket() as s:
    s.connect((HOST, PORT))
    s.send(b"Hello server!")   # client hello

    with open("received.txt", "wb") as f:
        while True:
            data = s.recv(1024)
            if not data:
                break
            f.write(data)

print("File received successfully")
```
## OUPUT
<img width="825" height="204" alt="Screenshot 2026-03-18 162254" src="https://github.com/user-attachments/assets/56690829-e50b-4c28-bf4d-c258fe4eecdc" />
<img width="826" height="112" alt="Screenshot 2026-03-18 162308" src="https://github.com/user-attachments/assets/058b6fdf-abe2-401b-ac19-526661e9c536" />


## RESULT
Thus, the python program for creating File Transfer using TCP Sockets Links was 
successfully created and executed.
