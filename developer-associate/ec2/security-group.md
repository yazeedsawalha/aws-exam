# Firewalls and Security Groups for EC2 Instances

Security groups are fundamental for network security in AWS, controlling traffic into and out of EC2 instances.

---

## Security Groups Basics  
- **Allow Rules Only**: Security groups only contain **allow** rules (no explicit deny rules).  
- **Inbound/Outbound Traffic Control**:  
  - **Inbound**: Controls traffic from outside to the instance (e.g., accessing an EC2 instance from your computer).  
  - **Outbound**: Controls traffic from the instance to the outside (e.g., EC2 connecting to the internet).  
- **Reference by IP or Security Group**:  
  - Rules can reference **IP ranges** (IPv4/IPv6) or **other security groups**.  

### Example Rule Structure  
```
Type    Protocol    Port Range    Source  
SSH     TCP         22            192.168.1.1  
HTTP    TCP         80            0.0.0.0/0
```

---

## Key Features & Behavior  
1. **Attach to Multiple Instances**:  
   - A security group can be attached to **multiple EC2 instances** not one to one relationship 
   - An instance can belong to **multiple security groups**.  
2. **Region/VPC Bound**:  
   - Security groups are tied to a **specific region and VPC**.  
   - Switching regions or VPCs requires recreating security groups.  
3. **Firewall Outside EC2**:  
   - Blocked traffic **never reaches** the EC2 instance (e.g., timeout errors).  
   - If traffic is allowed but the application isn’t running, you get a **connection refused error**.  
4. **Default Behavior**:  
   - **Inbound**: **Blocked by default**.  
   - **Outbound**: **Allowed by default** (EC2 can initiate outbound connections).  

---

## Advanced Features: Referencing Security Groups  
- **Cross-Group Authorization**:  
  - Allow traffic from instances associated with **another security group** (e.g., load balancers).  
  - Example:  
    - **EC2 Instance A** (Security Group 1) allows inbound traffic from **Security Group 2**.  
    - **EC2 Instance B** (Security Group 2) can communicate with Instance A, regardless of IP addresses.  
- **Diagram Scenario**:  
  - Instance with Security Group 1 authorizes inbound traffic from Security Group 2.  
  - Any instance with Security Group 2 can access the first instance.  
  - Instances with Security Group 3 (not authorized) are blocked.  

---

## Critical Ports to Memorize  
| Port  | Protocol | Use Case                                      |  
|-------|----------|-----------------------------------------------|  
| 22    | SSH      | Secure Shell (Linux logins)                   |  
| 21    | FTP      | File Transfer Protocol (upload files)         |  
| 22    | SFTP     | Secure File Transfer over SSH                 |  
| 80    | HTTP     | Unsecured web traffic (e.g., `http://`)       |  
| 443   | HTTPS    | Secured web traffic (e.g., `https://`)        |  
| 3389  | RDP      | Remote Desktop Protocol (Windows logins)      | 


---

## Best Practices & Troubleshooting  
1. **Separate SSH Security Group**:  
   - Maintain a **dedicated security group for SSH** (port 22) to simplify access management.  
2. **Timeout vs. Connection Refused**:  
   - **Timeout**: Security group blocks traffic (e.g., wrong IP/port in inbound rules).  
   - **Connection Refused**: Traffic is allowed, but the application isn’t running.  
3. **Least Privilege**:  
   - Restrict IP ranges (e.g., avoid `0.0.0.0/0` for SSH unless testing).  