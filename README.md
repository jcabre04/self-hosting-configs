The directories in this repository hold the configuration files for the services I selfhost. 

These services are for personal and educational use. Their config files are made using `.yaml` for deployment using `docker compose`.

# Container and port mapping
Below is a summary of what host ports I've assigned to what containers. I made the starred (\*) container images:

| **Container** | **Host Port** | **Reverse Proxy URL** | **Description** |
|-----------|-----------|-------------------|-------------|
| Kavita | 50000 (HTTP) | read.home.lab | Kavita is an ebook, manga, and comic web browser reader for your media |
| **~~Trilium~~ Retired** | ~~50001 (HTTP)~~ | ~~notes.home.lab~~ | ~~Trilium is a knowledge base. Great for notes, journaling, and writing~~ |
| Homer | 50002 (HTTP) | dash.home.lab | Homer is a static webpage dashboard. Easy to customize |
| DrawIO | 50003 (HTTP) | draw.home.lab | DrawIO is a tool to create technical diagrams |
| **^ Unused** | ~~50004 (HTTPS)~~ |  | ^ |
| \* Fanfiction-to-eBook | 50005 (HTTP) | fte.home.lab | FTE is a custom app that creates eBooks from online stories |
| Soft Serve | 50006 (SSH) | x | Soft Serve is a super lightweight textual UI Git server |
| Monica | 50007 (HTTP) | monica.home.lab | Monica is a personal people index (CRM). Great for organizing job search contacts and reminders |
| Pi-hole | 50008 (HTTP) | dns.home.lab | Pi-hole is a DNS sinkhole that adds DNS, advertisement blocking, and more capabilities to the host server |
| ^ | 53 (DNS) | \- | ^ |
| **^ Unused** | ~~67 (DHCP)~~ | \- | ~~Optional port for DHCP capabilities~~ |
| Ngnix-proxy-manager | 50009 (HTTP) | proxy.home.lab | NPM is a reverse proxy with a GUI for management. Pi-Hole sends the homelab's urls here. Then, NPM sends web requests to the respective host port |
| ^ | 80 (HTTP) | \- | ^ |
| ^ | 443 (HTTPS) | \- | ^ |
| Nextcloud | 50010 (HTTP) | cloud.home.lab | Nextcloud is a Google Drive (cloud file management) replacement |
| Onlyoffice | 50011 (HTTP) | office.home.lab | Onlyoffice is a Microsoft Office replacement. Hooked to and used by Nextcloud. Not usable on its own |
| KinD Cluster | 50001 (HTTP) | \- | Kubernetes IN Docker is a tool to run Kubernetes clusters using Docker. The tool creates docker containers that behave as independent nodes in a k8s cluster. These 5 ports are open  for k8s testing + learning. Will update with more specifics as needed |
| ^ | 50002 (HTTP) | \- | ^ |
| ^ | 50003 (HTTP) | \- | ^ |
| ^ | 50004 (HTTP) | \- | ^ |
| ^ | 50005 (HTTP) | \- | ^ |

*Note*: I used ports starting at 50,000 because they fall within the [private use / ephemeral range](https://en.wikipedia.org/wiki/Ephemeral_port). Known protocols, services, and products should not conflict with these ports. 50,000 is also an easy number to remember.

# Deploying
To deploy a service with the given config file, do the following:
1) make sure `docker` is installed
2) `cd` to the desired service's directory
    * if a service requires sensitive information (e.g., passwords, usernames) to deploy it, create a file called `.env` in the service directory and fill it with one variable per line.
    * example: `MYSQL_USERNAME=test-user`
3) run `docker compose up -d`
4) test access by going to the approprioate url. 
    * `localhost:PORT#`

For `kind`:
1) make sure `kind` and `kubectl` are installed
2) cd to the `kind` directory
3) run `kind create cluster --config my_default_kind_config.yaml`
4) verify with `kubectl cluster-info`. The Kubernetes control plane and CoreDNS should be running

# TO-DOs
- [ ] Finish Python cli tool that deploys all services or the given service