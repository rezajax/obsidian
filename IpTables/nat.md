
forwarding a port -> port


### Traffic Forwarding with iptables

#### Example: Forward Traffic from One Port to Another IP

Objective: Forward all traffic received on port `8080` of the server to another server with IP `192.168.1.100` on port `80`.

---

#### 1. Enable IP Forwarding:

To allow traffic forwarding, enable `IP Forwarding`:

- Temporary (until reboot):
    
    ```
    sudo sysctl -w net.ipv4.ip_forward=1
    ```
    
- Permanent: Add or ensure the following line exists in `/etc/sysctl.conf`:
    
    ```
    net.ipv4.ip_forward=1
    ```
    
    Then reload with:
    
    ```
    sudo sysctl -p
    ```
    

---

#### 2. Configure NAT Rule in iptables:

Use the `nat` table and the `PREROUTING` chain to modify the traffic destination:

```
sudo iptables -t nat -A PREROUTING -p tcp --dport 8080 -j DNAT --to-destination 192.168.1.100:80
```

Explanation:

- `-t nat`: Specifies the NAT table.
    
- `-A PREROUTING`: Appends the rule to the `PREROUTING` chain.
    
- `-p tcp`: Specifies the `TCP` protocol.
    
- `--dport 8080`: Matches traffic destined for port `8080`.
    
- `-j DNAT`: Performs Destination NAT.
    
- `--to-destination 192.168.1.100:80`: Specifies the new destination (IP and port).
    

---

#### 3. Allow Forwarding Traffic:

To permit forwarding of the traffic, add this rule to the `FORWARD` chain:

```
sudo iptables -A FORWARD -p tcp -d 192.168.1.100 --dport 80 -j ACCEPT
```

---

#### 4. Save Rules Permanently:

Ensure rules persist after reboot:

1. Install the `iptables-persistent` package:
    
    ```
    sudo apt install iptables-persistent
    ```
    
2. Save the current iptables rules:
    
    ```
    sudo netfilter-persistent save
    ```
    

---

### Exercise:

1. Configure similar forwarding for UDP traffic on port `53` (DNS).
    
2. Write a rule to forward traffic from port `22` (SSH) to a different port on the same server.