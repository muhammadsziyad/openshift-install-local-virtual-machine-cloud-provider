# openshift-install-local-virtual-machine-cloud-provider

Installing OpenShift can vary depending on the type of environment you are targeting (local development, virtual machines, or production-grade clusters on cloud platforms). Below, I'll outline the steps for installing OpenShift in a few different environments:

### 1. Installing OpenShift Locally with CodeReady Containers (CRC)

CodeReady Containers (CRC) is the quickest way to get OpenShift running on a local machine for development and testing purposes. CRC provides a minimal OpenShift 4 cluster in a VM.

#### Prerequisites

- A 4-core CPU
- 8 GB of RAM
- 35 GB of free disk space
- Virtualization support enabled in the BIOS
- Hypervisor installed (Hyper-V for Windows, libvirt for Linux, or HyperKit for macOS)

#### Installation Steps

1. **Download CodeReady Containers (CRC):**
    
    - Visit the CodeReady Containers download page and download the appropriate version for your operating system.
2. **Install CRC:**
    
    - Extract the CRC binary and move it to a directory in your PATH.
    
    **For Linux/macOS:**
    
    
    ```bash
    tar -xvf crc-linux-amd64.tar.xz sudo mv crc-linux-*-amd64/crc /usr/local/bin/
    ```
    
    **For Windows:**
    
    - Extract the downloaded archive and move `crc.exe` to a directory in your PATH.
3. **Set Up CRC:**
    
    - Run the CRC setup command to configure the environment:

	```bash
	crc setup
	```
    
4. **Start CRC:**
    
    - Start the OpenShift cluster:
    
    ```bash
    crc start
    ```
    
    - You will be prompted to enter a pull secret. You can obtain the pull secret from the Red Hat OpenShift Cluster Manager pull secret page.
5. **Access OpenShift:**
    
    - After CRC starts, you can access the OpenShift web console at the URL provided in the terminal output. The default credentials are usually `kubeadmin` with a generated password.

### 2. Installing OpenShift on Virtual Machines (using OKD)

OKD (Origin Kubernetes Distribution) is the community edition of OpenShift. It can be installed on virtual machines using tools like `openshift-installer`.

#### Prerequisites

- Linux virtual machines (bare metal or cloud VMs)
- DNS and DHCP configured for your VMs
- At least 4 CPUs, 8 GB of RAM, and 120 GB of storage per node

#### Installation Steps

1. **Download the OpenShift Installer:**
    
    - Visit the [OKD release page](https://github.com/openshift/okd/releases) and download the installer for your OS.
2. **Extract the Installer:**
    
    
```bash
tar -xvf openshift-install-linux.tar.gz sudo mv openshift-install /usr/local/bin/
```
    
3. **Generate Install Config:**
    
    - Run the installer to generate an install configuration:
    ```bash
    openshift-install create install-config --dir=<installation_directory>
	```
    
    - Follow the prompts to provide cluster information like cluster name, base domain, pull secret, and platform (e.g., bare metal or cloud provider).
4. **Create the Cluster:**
    - With the configuration generated, create the cluster:
```
openshift-install create cluster --dir=<installation_directory> --log-level=info
```
This process may take several minutes as it sets up the control plane and worker nodes.

5. **Access the Cluster:**
    
    - Once the installation is complete, the console URL and the kubeadmin credentials will be displayed.

### 3. Installing OpenShift on Cloud Providers

OpenShift can also be installed on major cloud providers like AWS, Azure, and Google Cloud using the same `openshift-installer` tool, but with cloud-specific configurations.

#### AWS Example Installation

1. **Download the OpenShift Installer:**
    
    - Download and extract the installer as described in the OKD section.
2. **Set Up AWS Credentials:**
    
    - Configure your AWS CLI with the necessary permissions for creating instances, VPCs, and other resources.
    ```
    aws configure
    ```
    
3. **Generate Install Config:**
    
    - Create the install config file for AWS:
    ```bash
    openshift-install create install-config --dir=<installation_directory>
	```

    
    - Specify AWS as the platform and provide details such as region, instance type, and networking.
4. **Create the Cluster:**
    
    - Start the installation process:

    
    ```bash
    openshift-install create cluster --dir=<installation_directory> --log-level=info
    ```
    
5. **Access the Cluster:**
    
    - After the installation completes, the console URL and kubeadmin credentials will be provided.

### Summary

OpenShift installation can range from a simple local setup with CodeReady Containers to a full-fledged production cluster on VMs or cloud providers. Choose the method that best suits your development, testing, or production needs.

If you need detailed instructions for a specific environment or encounter any issues during installation, feel free to ask!
