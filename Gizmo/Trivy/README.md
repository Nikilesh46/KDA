Update
#### Aqua Trivy ####

Trivy is a comprehensive security scanner. It is reliable, fast, extremely easy to use, and it works wherever you need it.
Trivy has different scanners that look for different security issues, and different targets where it can find those issues.

Targets:

Container Image
Filesystem
Git repository (remote)
Kubernetes cluster or resource
Scanners:

OS packages and software dependencies in use (SBOM)
Known vulnerabilities (CVEs)
IaC misconfigurations
Sensitive information and secrets

It is designed to be used in CI. Before pushing to a container registry or deploying your application, you can scan your local container image and other artifacts easily.




#### Installation #####

##### Adding Repository #####

sudo apt-get install wget apt-transport-https gnupg lsb-release

wget -qO - https://aquasecurity.github.io/trivy-repo/deb/public.key | gpg --dearmor | sudo tee /usr/share/keyrings/trivy.gpg > /dev/null

echo "deb [signed-by=/usr/share/keyrings/trivy.gpg] https://aquasecurity.github.io/trivy-repo/deb $(lsb_release -sc) main" | sudo tee -a /etc/apt/sources.list.d/trivy.list

sudo apt-get update

sudo apt-get install trivy


### Example Commands ###


trivy image imagename

trivy fs --security-checks vuln,config   Folder_name_OR_Path

trivy image --severity HIGH,CRITICAL image_name

trivy image -f json -o results.json image_name

trivy repo repo-url

trivy k8s --report summary cluster

