### Guide to Running a Full Node on Airchains' Junction

---

#### **System Requirements**
Before running a full node, ensure your system meets the following minimum requirements:

- **CPU**: 4 cores or more
- **RAM**: 8 GB or more
- **Disk**: 200 GB SSD (or more for mainnet nodes)
- **OS**: Linux (Ubuntu 20.04 recommended) or macOS
- **Network**: Stable internet connection with open ports for communication

---

### **Step 1: Installing Dependencies**

Ensure the following dependencies are installed:
- Git
- Docker
- Docker Compose

You can install these by running the commands below:

```bash
# Update package list
sudo apt update

# Install Git
sudo apt install git -y

# Install Docker
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh

# Add current user to the Docker group
sudo usermod -aG docker ${USER}

# Install Docker Compose
sudo apt install docker-compose -y
```

After installation, log out and back in to activate Docker for your user.

---

### **Step 2: Cloning the Airchains Junction Repository**

Clone the repository for Airchains Junction to access the required files.

```bash
git clone https://github.com/airchains/junction.git
cd junction
```

---

### **Step 3: Configuring the Node**

1. Inside the `junction` directory, there should be configuration files provided by Airchains.
2. Modify the `.env` file (if available) to set up any specific configurations. Adjust fields like node name, network type, and any other required fields. Here's an example template:

```bash
# Example .env file

NODE_NAME="your_node_name"
NETWORK="mainnet" # Change to "testnet" if running on testnet
RPC_PORT=8545
P2P_PORT=30303
```

3. Save the file after making the necessary changes.

---

### **Step 4: Running the Node with Docker Compose**

Airchains likely provides a Docker Compose file to manage and run the node as a service. Start the full node by running the following command:

```bash
docker-compose up -d
```

The `-d` flag runs the services in detached mode, allowing them to run in the background.

---

### **Step 5: Verifying Node Operation**

To ensure your node is up and running:

1. Check running containers:

    ```bash
    docker ps
    ```

   You should see containers running for your Airchains node.

2. Verify logs to ensure no errors:

    ```bash
    docker logs -f <container_id>
    ```

   Replace `<container_id>` with the actual container ID from `docker ps`.

3. You can also verify the node by checking if it's syncing with the network or interacting with it. Use an HTTP request or any CLI tool that interfaces with the node’s API, usually at `http://localhost:8545` (default RPC port).

---

### **Step 6: Managing and Updating the Node**

To stop the node:

```bash
docker-compose down
```

To update the node, pull the latest changes from the repository, rebuild the Docker containers, and restart:

```bash
git pull origin main
docker-compose down
docker-compose up -d --build
```

---

### **Troubleshooting**

If you encounter any issues, try the following:

- Ensure Docker is running and your user has access to it.
- Check your `.env` configuration to confirm network and node details are accurate.
- Refer to Airchains documentation for any specific error messages or join their support channels for assistance.
