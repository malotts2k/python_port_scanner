# A quick port scanner I spun up in Python. 

This is a really fantastic portable tool to quickly scan the open ports on a host. It only took a few minutes of breezing through tutorials and reading stackexchange to find the code to bolt together to actually make this work.

I've uploaded the Python script in this repo but the raw code to execute this code can be found at the bottom of this entry.  I've also included a screenshot of the structure of the code and how it's built out for reference.

![image](https://user-images.githubusercontent.com/105020710/186779826-e59d2ddf-a2cb-4366-afc6-001a4cf86703.png)


The end result of the script (depending on the port range and amount of threads defined) look like this:

![image](https://user-images.githubusercontent.com/105020710/186779444-56cb1821-d0b9-43a6-88a2-242dd1127de4.png)


<br>
<br>
<br>
<br>


The raw code:

import socket
import threading
from queue import Queue

target = "10.0.0.138"
queue = Queue()
open_ports = []


def portscan(port):
    try:
        sock = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
        sock.connect((target, port))
        return True

    except:
        return False


def fill_queue(port_list):
    for port in port_list:
        queue.put(port)

def worker():
    while_not queue.empty():
        port = queue.get()
        if portscan(port):
            print("Port {} is open.".format(port))
            open_ports.append{port}


port_list = range(1, 1024)
fill_queue(port_list)

thread_list = []

for t in range(100):
    thread = threading.Thread(target=worker)
    thread_list.append(thread)

for thread in thread_list:
    thread.start()

for thread in thread_list:
    thread.join()

print("Open ports are: ", open_ports)
