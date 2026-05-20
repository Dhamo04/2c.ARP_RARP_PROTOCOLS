# 2c.SIMULATING ARP /RARP PROTOCOLS
## AIM
To write a python program for simulating ARP protocols using TCP.
## ALGORITHM:
## Client:
1. Start the program
2. Using socket connection is established between client and server.
3. Get the IP address to be converted into MAC address.
4. Send this IP address to server.
5. Server returns the MAC address to client.
## Server:
1. Start the program
2. Accept the socket which is created by the client.
3. Server maintains the table in which IP and corresponding MAC addresses are
stored.
4. Read the IP address which is send by the client.
5. Map the IP address with its MAC address and return the MAC address to client.
P
## PROGRAM - ARP
server side
```
import socket
s=socket.socket()
s.connect(('localhost',8000))
while True:
    ip=input("Enter logical Address : ")
    s.send(ip.encode())
    print("MAC Address",s.recv(1024).decode())
```
client side
```
import socket
s=socket.socket()
s.bind(('localhost',8000))
s.listen(5)
c,addr=s.accept()
address={"165.165.80.80":"6A:08:AA:C2","165.165.79.1":"8A:BC:E3:FA"};
while True:
    ip=c.recv(1024).decode()
    try:
        c.send(address[ip].encode())
    except KeyError:
        c.send("Not Found".encode())
```
## OUPUT - ARP
<img width="926" height="256" alt="Screenshot 2026-05-20 082921" src="https://github.com/user-attachments/assets/e5273269-7dc7-4f42-bfce-3cf267d68781" />

## PROGRAM - RARP
server side
```
import socket

s = socket.socket()
s.bind(('localhost', 9000))
s.listen(5)

print("Server waiting...")

c, addr = s.accept()
print("Connected to", addr)

address = {
    "6A:08:AA:C2": "192.168.1.100",
    "8A:BC:E3:FA": "192.168.1.99"
}

while True:
    mac = c.recv(1024).decode()

    if not mac:
        break

    try:
        c.send(address[mac].encode())
    except KeyError:
        c.send("Not Found".encode())

c.close()
s.close()
```
client side
```
import socket

s = socket.socket()
s.connect(('localhost', 9000))

while True:
    mac = input("Enter MAC Address : ")

    if mac == "exit":
        break

    s.send(mac.encode())
    print("Logical Address:", s.recv(1024).decode())

s.close()
```

## OUPUT -RARP
<img width="923" height="167" alt="Screenshot 2026-05-20 084241" src="https://github.com/user-attachments/assets/cfe6981e-01b2-491b-b8fd-2c876a7605d7" />

## RESULT
Thus, the python program for simulating ARP protocols using TCP was successfully 
executed.
