from ping3 import ping
import socket

def scan_network(ip_range, range_size=10):
    devices = []
    ip_base = ip_range.split('/')[0]
    base_parts = ip_base.split('.')
    ip_prefix = f"{base_parts[0]}.{base_parts[1]}.{base_parts[2]}."
    start_ip = int(base_parts[3])
    end_ip = min(start_ip + range_size, 255)  # Ensure we don't exceed 255

    for i in range(start_ip, end_ip):
        ip = f"{ip_prefix}{i}"
        try:
            # Send an ICMP ping request
            response_time = ping(ip, timeout=1)
            if response_time is not None:
                hostname = "Unknown"
                try:
                    hostname = socket.gethostbyaddr(ip)[0]
                except socket.herror:
                    pass  # Keep "Unknown" if hostname resolution fails

                devices.append((ip, hostname))
        except Exception as e:
            print(f"An error occurred while scanning IP {ip}: {e}")

    return devices

def display_results(devices):
    print("IP Address\t\tHostname")
    print("-" * 50)
    for ip, hostname in devices:
        print(f"{ip:<15}\t{hostname}")

def main():
    ip_range = "xxx.xxx.x.x/xx"  # Change this to your network's IP range (example: " 129.186.55.0/24 ")
    try:
        devices = scan_network(ip_range)

        if devices:
            display_results(devices)
        else:
            print("No devices found.")
    except Exception as e:
        print(f"An error occurred in the main function: {e}")

if __name__ == "__main__":
    print("scanning for ip")
    main()
