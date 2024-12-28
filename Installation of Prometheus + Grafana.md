### **Installation Guide for Prometheus, Blackbox Exporter, and Grafana**

---

### **1. Prometheus Installation**
Prometheus is a powerful open-source monitoring and alerting toolkit.

#### **Step 1: Download Prometheus**
1. Visit the [Prometheus Downloads page](https://prometheus.io/download/).
2. Use the following `wget` command to download the latest Prometheus tarball:
   ```bash
   wget https://github.com/prometheus/prometheus/releases/download/v3.1.0-rc.0/prometheus-3.1.0-rc.0.linux-amd64.tar.gz
   ```

#### **Step 2: Extract the Tarball**
3. Extract the downloaded file:
   ```bash
   tar -xvzf prometheus-3.1.0-rc.0.linux-amd64.tar.gz
   mv prometheus-3.1.0-rc.0.linux-amd64 prometheus-3.1.0
   cd prometheus-3.1.0
   ```

#### **Step 3: Configure Prometheus**
4. Create a directory for Prometheus files:
   ```bash
   sudo mkdir /etc/prometheus
   sudo mkdir /var/lib/prometheus
   ```
5. Move binaries and configuration files:
   ```bash
   sudo mv prometheus /usr/local/bin/
   sudo mv promtool /usr/local/bin/
   sudo mv prometheus.yml /etc/prometheus/
   ```

#### **Step 4: Start Prometheus**
6. Run Prometheus manually (for testing):
   ```bash
   prometheus --config.file=/etc/prometheus/prometheus.yml
   ```
7. To run Prometheus as a service:
   - Create a Prometheus service file:
     ```bash
     sudo nano /etc/systemd/system/prometheus.service
     ```
   - Add the following content:
     ```ini
     [Unit]
     Description=Prometheus Monitoring System
     Wants=network-online.target
     After=network-online.target

     [Service]
     User=prometheus
     ExecStart=/usr/local/bin/prometheus --config.file=/etc/prometheus/prometheus.yml --storage.tsdb.path=/var/lib/prometheus

     [Install]
     WantedBy=multi-user.target
     ```
   - Reload systemd and start the service:
     ```bash
     sudo systemctl daemon-reload
     sudo systemctl start prometheus
     sudo systemctl enable prometheus
     ```

#### **Step 5: Verify Installation**
8. Access Prometheus in your browser at:  
   ```
   http://<server-ip>:9090
   ```

---

### **2. Blackbox Exporter Installation**
The Blackbox Exporter allows Prometheus to monitor endpoints over HTTP, HTTPS, and other protocols.

#### **Step 1: Download Blackbox Exporter**
1. Download the latest Blackbox Exporter tarball:
   ```bash
   wget https://github.com/prometheus/blackbox_exporter/releases/download/v0.25.0/blackbox_exporter-0.25.0.linux-amd64.tar.gz
   ```

#### **Step 2: Extract the Tarball**
2. Extract the downloaded file:
   ```bash
   tar -xvzf blackbox_exporter-0.25.0.linux-amd64.tar.gz
   cd blackbox_exporter-0.25.0.linux-amd64
   ```

#### **Step 3: Run Blackbox Exporter**
3. Run the Blackbox Exporter:
   ```bash
   ./blackbox_exporter
   ```
4. To run it as a service, create a service file similar to the one for Prometheus, but update the executable path to `blackbox_exporter`.

---

### **3. Grafana Installation**
Grafana is a visualization tool for monitoring data.

#### **Step 1: Install Dependencies**
1. Install required packages:
   ```bash
   sudo apt-get update
   sudo apt-get install -y adduser libfontconfig1 musl
   ```

#### **Step 2: Download Grafana**
2. Download the Grafana Enterprise Debian package:
   ```bash
   wget https://dl.grafana.com/enterprise/release/grafana-enterprise_11.4.0_amd64.deb
   ```

#### **Step 3: Install Grafana**
3. Install the package:
   ```bash
   sudo dpkg -i grafana-enterprise_11.4.0_amd64.deb
   ```

#### **Step 4: Start Grafana**
4. Enable and start the Grafana service:
   ```bash
   sudo systemctl start grafana-server
   sudo systemctl enable grafana-server
   ```

#### **Step 5: Access Grafana**
5. Open Grafana in your browser at:
   ```
   http://<server-ip>:3000
   ```
6. Log in with default credentials:
   - Username: `admin`
   - Password: `admin` (you'll be prompted to change this after logging in).

---

### **4. Configuring Prometheus with Grafana**
1. Log in to Grafana and go to **Configuration > Data Sources**.
2. Add a new data source:
   - Type: **Prometheus**
   - URL: `http://<prometheus-ip>:9090`
3. Click **Save & Test** to confirm connectivity.

---

### **5. Notes**
- Ensure all services have the proper firewall rules to allow external access (e.g., ports 9090 for Prometheus, 3000 for Grafana).
- Use strong passwords and restrict access to these services in production environments.

With Prometheus, Blackbox Exporter, and Grafana installed, you can now set up dashboards to visualize and monitor your system metrics effectively!
