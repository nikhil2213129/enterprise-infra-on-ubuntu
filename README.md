# Mastering Linux Network Services: A Hands-On Guide to DNS, HTTP, NFS & MySQL Deployments

## 📌 Overview
This project demonstrates a **complete corporate network infrastructure** implemented on Ubuntu servers, with emphasis on **resilience, security, and scalability**. It covers essential services that power modern IT environments—ideal for **SysAdmins, DevOps engineers, and campus placement preparation**.

---

## 🌐 DNS Deployment Essentials
- **Service:** BIND9 for authoritative name resolution  
- **Setup:**  
  - Primary servers for corporate/technical zones + departmental subdomains  
  - Static IP assignment via **netplan**  
  - Zone files with **A, CNAME, PTR records** for web, DB, and storage services  
  - `named.conf.local` restrictions for secure zone transfers  
- **Best Practices:**  
  - Tune **SOA records** for efficient slave synchronization  
  - Whitelist secondary servers only  
  - Validate with `dig` and test unauthorized AXFR denials  

---

## ⚡ HTTP Server Farm with Load Balancing
- **Cluster:** Apache2 with PHP modules across multiple nodes  
- **Virtual Hosts:** External sites, intranets, and user webspaces (PHP enabled selectively via `mod_userdir`)  
- **Load Distribution:** DNS round-robin with multiple A records per hostname  
- **Resilience:**  
  - Shared storage mounted with soft timeouts/interrupts  
  - Uniform virtual host configs across nodes  
  - Monitor via `systemctl`  

---

## 📂 NFS for Centralized Shared Storage
- **Exports:** Limited to web server IPs with RW + synchronous writes  
- **Client Mounts:** Automated via `fstab` for boot-time consistency  
- **Security:**  
  - Reverse DNS verification with PTR records  
  - `hosts.allow` rules for trusted domains  
- **Scalability:** Replication-ready secondaries for high availability  

---

## 🛡️ Secure MySQL Database Infrastructure
- Harden with `mysql_secure_installation` (disable anonymous access, remote root)  
- Bind listeners to **localhost/internal interfaces**  
- Create **dedicated DBs and users** with granular GRANTs (no wildcards)  
- Restrict PhpMyAdmin access to **admin subnets**, enforce TLS + cookie auth  
- Automate provisioning with scripts (UTF8 collation, privilege assignment, `FLUSH PRIVILEGES`)  
- Audit with `SHOW GRANTS`  

---

## 🔧 Advanced Configuration & Troubleshooting
- **DNS:** Increment serials, reduce TTLs for faster propagation  
- **HTTP:** Trace DNS responses; plan session affinity for stateful apps  
- **NFS:** Verify exports with `showmount`; debug `hosts.allow` mismatches  
- **MySQL:** Check `bind-address` and firewall rules (`ufw allow 3306`)  

### Pro Commands
- **Network:** `ip addr`, `ss -tuln`, `journalctl -u named`  
- **Services:** `systemctl restart apache2`, `exportfs -ra`  
- **Security:** `ufw status verbose`, `mysqldump --single-transaction`  

---

## 🚀 Real-World Relevance & Next Steps
- Skills align with **enterprise web stacks** and **technical interviews**  
- Replicate via **VirtualBox/Multipass** for practice (isolate nets, break/fix iteratively)  
- Extend with:  
  - `iptables` for layered filtering  
  - **Nagios/Prometheus** for monitoring  
  - **Ansible** for Infrastructure-as-Code  
- Share sanitized templates (netplan YAMLs, NFS exports, MySQL scripts) on GitHub for **portfolio credibility**  

---

## 📖 Reference
[Project PDF](https://drive.google.com/file/d/1rXcsCqYbrepdHOV1-03XqSppnxpAx2TE/view?usp=drive_link)

---

**Deploy today, iterate tomorrow. Feedback welcome!**  
#LinuxNetworking #SysAdmin #DevOps #TechBlog
