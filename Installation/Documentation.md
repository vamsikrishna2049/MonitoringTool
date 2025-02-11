Certainly! Below is a clean, structured documentation on how to install and configure Prometheus and Grafana on Ubuntu 22.04 LTS, along with the necessary steps to visualize metrics with Grafana.

---

# **Prometheus and Grafana Installation Guide on Ubuntu 22.04 LTS**

## **Introduction**
This guide provides instructions to install **Prometheus** (a powerful open-source monitoring and alerting toolkit) and **Grafana** (a visualization platform) on Ubuntu 22.04 LTS. We will also cover how to set up Node Exporter for gathering system metrics and how to configure Grafana to visualize data from Prometheus.

### **Prerequisites**
- A server running **Ubuntu 22.04 LTS**
- Root or **sudo** privileges
- Open ports: `9090` (Prometheus), `3000` (Grafana), `9100` (Node Exporter)

---

## **Part 1: Install Prometheus**

### **Step 1: Install Prometheus Dependencies**

1. Update the system's repository index:
   ```bash
   sudo apt update -y
   ```

2. Install the required packages:
   ```bash
   sudo apt install wget curl tar -y
   ```

### **Step 2: Create Prometheus User and Directories**

1. Create the Prometheus user and group (without home directories):
   ```bash
   sudo useradd --no-create-home --shell /bin/false prometheus
   sudo mkdir /etc/prometheus
   sudo mkdir /var/lib/prometheus
   ```

2. Set the appropriate ownership for the directories:
   ```bash
   sudo chown prometheus:prometheus /etc/prometheus
   sudo chown prometheus:prometheus /var/lib/prometheus
   ```

### **Step 3: Download Prometheus**

1. Go to the [Prometheus Releases Page](https://github.com/prometheus/prometheus/releases) and find the download link for version `3.1.0` (or the desired version). 

2. Download the Prometheus tarball:
   ```bash
   cd /opt
   wget https://github.com/prometheus/prometheus/releases/download/v3.1.0/prometheus-3.1.0.linux-386.tar.gz
   ```

3. Verify the downloaded file:
   ```bash
   sha256sum prometheus-3.1.0.linux-386.tar.gz
   ```

4. Extract the downloaded file:
   ```bash
   tar -xvf prometheus-3.1.0.linux-386.tar.gz
   cd prometheus-3.1.0.linux-386
   ```

### **Step 4: Install Prometheus**

1. Copy the extracted files to the appropriate directories:
   ```bash
   sudo cp prometheus /usr/local/bin/
   sudo cp promtool /usr/local/bin/
   sudo cp -r consoles /etc/prometheus/
   sudo cp -r console_libraries /etc/prometheus/
   sudo cp prometheus.yml /etc/prometheus/
   ```

2. Set the correct permissions:
   ```bash
   sudo chown -R prometheus:prometheus /usr/local/bin/prometheus
   sudo chown -R prometheus:prometheus /usr/local/bin/promtool
   sudo chown -R prometheus:prometheus /etc/prometheus
   ```

### **Step 5: Configure Prometheus**

1. Open the `prometheus.yml` file:
   ```bash
   sudo nano /etc/prometheus/prometheus.yml
   ```

2. Ensure it has the following configuration (basic example):
   ```yaml
   global:
     scrape_interval: 15s

   scrape_configs:
     - job_name: 'prometheus'
       static_configs:
         - targets: ['localhost:9090']
   ```

### **Step 6: Create a Systemd Service for Prometheus**

1. Create a systemd service file for Prometheus:
   ```bash
   sudo nano /etc/systemd/system/prometheus.service
   ```

2. Add the following content:
   ```ini
   [Unit]
   Description=Prometheus
   After=network-online.target
   Wants=network-online.target

   [Service]
   User=prometheus
   Group=prometheus
   Type=simple
   ExecStart=/usr/local/bin/prometheus \
     --config.file /etc/prometheus/prometheus.yml \
     --storage.tsdb.path /var/lib/prometheus/ \
     --web.console.templates=/etc/prometheus/consoles \
     --web.console.libraries=/etc/prometheus/console_libraries

   [Install]
   WantedBy=multi-user.target
   ```

3. Reload the systemd manager to recognize the new service:
   ```bash
   sudo systemctl daemon-reload
   sudo systemctl start prometheus
   sudo systemctl enable prometheus
   ```

4. Check if Prometheus is running:
   ```bash
   sudo systemctl status prometheus
   ```

---

## **Part 2: Install Grafana**

### **Step 1: Install Grafana Using APT**

1. Add the Grafana APT repository:
   ```bash
   sudo apt-get install -y software-properties-common
   sudo add-apt-repository "deb https://packages.grafana.com/oss/deb stable main"
   wget -q -O - https://packages.grafana.com/gpg.key | sudo apt-key add -
   ```

2. Update the package list and install Grafana:
   ```bash
   sudo apt-get update
   sudo apt-get install grafana
   ```

3. Start and enable the Grafana service:
   ```bash
   sudo systemctl start grafana-server
   sudo systemctl enable grafana-server
   ```

4. Check the Grafana service status:
   ```bash
   sudo systemctl status grafana-server
   ```

### **Step 2: Access the Grafana Web Interface**

- Open your browser and navigate to `http://your_server_ip:3000`.
- Login with the default credentials:
  - **Username**: `admin`
  - **Password**: `admin`
- Change the password after logging in.

---

## **Part 3: Configure Grafana to Use Prometheus as a Data Source**

### **Step 1: Add Prometheus as a Data Source**

1. In the Grafana web interface, go to **Settings** (gear icon) -> **Data Sources**.
2. Click **Add data source** and select **Prometheus**.
3. Configure the Prometheus data source:
   - **URL**: `http://localhost:9090`
   - Leave other settings as default and click **Save & Test**.

### **Step 2: Create a Dashboard**

1. Click on the **+** icon in the left menu and choose **Dashboard**.
2. Click **Add Query** and select **Prometheus** from the data source dropdown.
3. Enter a Prometheus query, such as `up` to check if Prometheus is running.
4. Customize the dashboard as needed (e.g., add more queries, change visualization types).

---

## **Part 4: Install Node Exporter**

### **Step 1: Download and Install Node Exporter**

1. Download Node Exporter from the [Prometheus GitHub](https://github.com/prometheus/node_exporter/releases):
   ```bash
   wget https://github.com/prometheus/node_exporter/releases/download/v1.2.0/node_exporter-1.2.0.linux-amd64.tar.gz
   ```

2. Extract the file:
   ```bash
   tar -xvzf node_exporter-1.2.0.linux-amd64.tar.gz
   ```

3. Move the `node_exporter` binary to `/usr/local/bin`:
   ```bash
   sudo mv node_exporter-1.2.0.linux-amd64/node_exporter /usr/local/bin
   ```

### **Step 2: Create a Systemd Service for Node Exporter**

1. Create a systemd service file:
   ```bash
   sudo nano /etc/systemd/system/node_exporter.service
   ```

2. Add the following content:
   ```ini
   [Unit]
   Description=Prometheus Node Exporter
   After=network.target

   [Service]
   User=nobody
   ExecStart=/usr/local/bin/node_exporter

   [Install]
   WantedBy=multi-user.target
   ```

3. Enable and start the service:
   ```bash
   sudo systemctl daemon-reload
   sudo systemctl enable node_exporter
   sudo systemctl start node_exporter
   ```

4. Check the Node Exporter status:
   ```bash
   sudo systemctl status node_exporter
   ```

### **Step 3: Add Node Exporter as a Target in Prometheus**

1. Edit the `prometheus.yml` file:
   ```bash
   sudo nano /etc/prometheus/prometheus.yml
   ```

2. Add the Node Exporter target under `scrape_configs`:
   ```yaml
   scrape_configs:
     - job_name: 'prometheus'
       static_configs:
         - targets: ['localhost:9090']
     - job_name: 'node_exporter'
       static_configs:
         - targets: ['localhost:9100']
   ```

3. Restart Prometheus:
   ```bash
   sudo systemctl restart prometheus
   ```

---

## **Conclusion**
You have successfully installed Prometheus, Grafana, and Node Exporter on Ubuntu 22.04 LTS. You can now use Grafana to visualize metrics from Prometheus and monitor your system's performance using Node Exporter.

### **Further Enhancements**
- Set up alerts in Prometheus to notify you of system issues.
- Create more detailed Grafana dashboards using additional Prometheus metrics.
- Customize the Prometheus `prometheus.yml` file to scrape other services and resources.

---

Let me know if you'd like any specific modifications to this documentation!
