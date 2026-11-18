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
Client Side
~~~
import socket

s = socket.socket()
s.connect(('localhost', 8000))

while True:
    ip = input("Enter IP Address: ")

    s.sendall(ip.encode())

    if ip == "exit":
        break

    mac = s.recv(1024).decode()

    print("MAC Address:", mac)

s.close()
~~~
Server Side
~~~
import socket

s = socket.socket()
s.bind(('localhost', 8000))
s.listen(5)

print("ARP Server Started...")
c, addr = s.accept()

address = {
    "192.168.1.1": "AA:BB:CC:11",
    "192.168.1.2": "AA:BB:CC:22",
    "192.168.1.3": "AA:BB:CC:33"
}

while True:
    ip = c.recv(1024).decode()

    if ip == "exit":
        break

    if ip in address:
        mac = address[ip]
    else:
        mac = "Not Found"

    c.sendall(mac.encode())

c.close()
s.close()
~~~
## OUPUT - ARP
<img width="1895" height="905" alt="Screenshot 2026-11-18 084337" src="https://github.com/user-attachments/assets/3132aaaa-c1c6-4fc0-b96f-89455e37a0fa" />

## PROGRAM - RARP
Client Side
~~~
import socket

s = socket.socket()
s.connect(('localhost', 9000))

while True:
    mac = input("Enter MAC Address: ")

    s.sendall(mac.encode())

    if mac == "exit":
        break

    ip = s.recv(1024).decode()

    print("Logical Address:", ip)

s.close()
~~~
Server Side
~~~
import socket

s = socket.socket()
s.bind(('localhost', 9000))
s.listen(5)

print("RARP Server Started...")
c, addr = s.accept()

address = {
    "AA:BB:CC:11": "192.168.1.1",
    "AA:BB:CC:22": "192.168.1.2",
    "AA:BB:CC:33": "192.168.1.3"
}

while True:
    mac = c.recv(1024).decode()

    if mac == "exit":
        break

    if mac in address:
        ip = address[mac]
    else:
        ip = "Not Found"

    c.sendall(ip.encode())

c.close()
s.close()
~~~
## OUPUT -RARP
<img width="1880" height="912" alt="image" src="https://github.com/user-attachments/assets/682a31db-80be-4baa-96b1-514b68f9ed90" />

## RESULT
Thus, the python program for simulating ARP protocols using TCP was successfully 
executed.
