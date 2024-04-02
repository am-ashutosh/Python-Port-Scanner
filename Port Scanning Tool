import socket
import threading

def scan_ports(target, start_port, end_port):
    print(f"Scanning ports on {target}...")
    open_ports = []

    def check_port(port):
        sock = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
        sock.settimeout(1)
        result = sock.connect_ex((target, port))
        if result == 0:
            open_ports.append(port)
            print(f"Port {port} is open")
        sock.close()

    threads = []
    for port in range(start_port, end_port + 1):
        thread = threading.Thread(target=check_port, args=(port,))
        threads.append(thread)
        thread.start()

    # Wait for all threads to finish
    for thread in threads:
        thread.join()

    if open_ports:
        print("Open ports:", open_ports)
    else:
        print("No open ports found.")

if __name__ == "__main__":
    target_host = input("Enter the target website or IP address: ")

    try:
        start_port = int(input("Enter the starting port: "))
        end_port = int(input("Enter the ending port: "))
    except ValueError:
        print("Invalid port number. Please enter a valid integer.")
    else:
        scan_ports(target_host, start_port, end_port)
