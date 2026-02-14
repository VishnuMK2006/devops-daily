# AWS CLI setup
##  Install AWS CLI

Check:

```bash
aws --version
```

If missing:

```bash
sudo apt install awscli
```


# Configure AWS Credentials

Terraform needs AWS access.

Run:

```bash
aws configure
```

Enter:

```
AWS Access Key ID
AWS Secret Access Key
Region (example: ap-south-1)
Output format → json
```

Credentials stored in:

```
~/.aws/credentials
```
### AWS used creation and access key creation
#### create new user
<img width="1917" height="870" alt="Screenshot from 2026-02-14 08-49-14" src="https://github.com/user-attachments/assets/ea837112-0522-4936-bb96-f0f0fbd80792" />

#### Choose the attach polices directly(Not **Add user to group*) 

<img width="1917" height="870" alt="Screenshot from 2026-02-14 08-50-28" src="https://github.com/user-attachments/assets/ead9407b-d112-46a9-886d-47276bd0c32a" />

#### Select the AdminstratorAccess

<img width="1917" height="870" alt="Screenshot from 2026-02-14 08-51-40" src="https://github.com/user-attachments/assets/69e22c31-d3c1-486a-81e7-c2e8bf7796af" />

*Download the access key and secrete key tokens**

# Terraform Setup


## 1. Prerequisites

Before installing Terraform, ensure your system is updated and required packages are installed.

```bash
sudo apt-get update
sudo apt-get install -y gnupg software-properties-common
```

**Explanation:**

* `apt-get update`
  Refreshes your system’s package list so Ubuntu knows about the latest available software versions.

* `apt-get install gnupg software-properties-common`

  * **gnupg**: Used to verify HashiCorp’s GPG key (security validation).
  * **software-properties-common**: Helps manage repositories.


<img width="1130" height="1140" alt="Screenshot from 2026-02-14 08-42-37" src="https://github.com/user-attachments/assets/d103d484-adec-4565-a716-973bea42d6d9" />

## 2. Add HashiCorp GPG Key

```bash
wget -O- https://apt.releases.hashicorp.com/gpg | \
gpg --dearmor | \
sudo tee /usr/share/keyrings/hashicorp-archive-keyring.gpg > /dev/null
```

**Explanation:**

* Downloads HashiCorp’s official signing key.
* Converts it into a format Ubuntu understands.
* Stores it securely so packages from HashiCorp can be verified.

This ensures Terraform packages are authentic and not tampered with.



## 3. Verify GPG Fingerprint (Optional but Recommended)

```bash
gpg --no-default-keyring \
--keyring /usr/share/keyrings/hashicorp-archive-keyring.gpg \
--fingerprint
```

**Explanation:**

* Displays the fingerprint of the imported key.
* Lets you confirm it matches HashiCorp’s official fingerprint.

This step improves security but can be skipped if you trust the source.


## 4. Add HashiCorp Repository

```bash
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] \
https://apt.releases.hashicorp.com \
$(grep -oP '(?<=UBUNTU_CODENAME=).*' /etc/os-release || lsb_release -cs) main" \
| sudo tee /etc/apt/sources.list.d/hashicorp.list
```

**Explanation:**

* Adds HashiCorp’s official repository to your system.
* Allows Ubuntu to fetch Terraform directly from HashiCorp.


## 5. Update Package List Again

```bash
sudo apt update
```

**Explanation:**

Refreshes package information including the newly added HashiCorp repository.



## 6. Install Terraform

```bash
sudo apt-get install terraform
```

**Explanation:**

Installs Terraform on your system.

Verify installation:

```bash
terraform -version
```


<img width="1920" height="1117" alt="Screenshot from 2026-02-13 22-27-58" src="https://github.com/user-attachments/assets/a4bb86ed-4896-4c23-aa27-20a9e4bb5e3d" />

# Instance creation by using terraform

## 1. Clone the Repository

```bash
git clone https://github.com/jagadeeshkanna97/terraform-dev.git
cd terraform-dev
```

**Explanation:**

* Downloads the Terraform project files.
* Moves into the project directory.

---

## 2. Modify Variables

Edit `variable.tf` according to your requirements.

```bash
nano variable.tf
```

**Explanation:**

Variables allow you to customize values like:

* Region
* Instance type
* Tags
* Credentials (if applicable)

---

# Terraform Commands Explained

---

## 1. `terraform init`

```bash
terraform init
```

**Purpose:**

Initializes the Terraform project.

**What it does:**

* Downloads required provider plugins (AWS, Azure, etc.).
* Sets up backend (if configured).
* Prepares working directory.

Run this **only once per project** or after adding/changing providers.

<img width="1920" height="1200" alt="Screenshot from 2026-02-14 09-34-26" src="https://github.com/user-attachments/assets/acc31093-edc1-4945-99af-1ca6ccbd262e" />

---

## 2. `terraform plan`

```bash
terraform plan
```

**Purpose:**

Shows what Terraform *will do* before making changes.

**What it does:**

* Compares current infrastructure vs configuration files.
* Displays:

  * Resources to be created
  * Resources to be modified
  * Resources to be destroyed

This is a preview step. No changes are made.

<img width="1920" height="1200" alt="Screenshot from 2026-02-14 09-34-32" src="https://github.com/user-attachments/assets/3d293bd3-d3ac-4b7e-8e24-088d445f0136" />

---

## 3. `terraform apply`

```bash
terraform apply
```

**Purpose:**

Creates or updates infrastructure.

**What it does:**

* Executes the plan.
* Provisions resources (VMs, networks, storage, etc.).

Terraform will ask for confirmation before proceeding.

<img width="1920" height="1200" alt="Screenshot from 2026-02-14 09-34-38" src="https://github.com/user-attachments/assets/65d1872c-42a8-4ba7-abf9-5da101e0ea22" />
<img width="1920" height="1200" alt="Screenshot from 2026-02-14 09-34-43" src="https://github.com/user-attachments/assets/afb02473-b6c3-4a4d-8727-febb3ca2b47c" />
<img width="1920" height="1200" alt="Screenshot from 2026-02-14 09-34-47" src="https://github.com/user-attachments/assets/555c316c-5ebf-475d-881c-e899798d69a5" />
---


### AWS instance dashboard.(*Created by terraform*)

<img width="1920" height="1200" alt="Screenshot from 2026-02-14 09-34-52" src="https://github.com/user-attachments/assets/cc549d89-803b-4e2f-b5d9-df159690a587" />



## 4. `terraform destroy`

```bash
terraform destroy
```

**Purpose:**

Deletes all resources managed by Terraform.

**What it does:**

* Safely removes infrastructure created via Terraform.

Use this when:

* Cleaning up
* Avoiding unnecessary cloud costs
* Rebuilding environment

<img width="1920" height="1200" alt="Screenshot from 2026-02-14 09-38-43" src="https://github.com/user-attachments/assets/8719a48f-8d35-4b7f-b90a-06c06a6a36f1" />


## Destroted by the *Terraform.*
<img width="1920" height="1200" alt="Screenshot from 2026-02-14 09-38-53" src="https://github.com/user-attachments/assets/4f8a729d-2243-410f-9bed-1807a6cac3c6" />

---

# Terraform Explained:

Terraform is an **Infrastructure as Code (IaC)** tool.

Instead of manually creating servers and networks in the cloud:

You write configuration files describing:

* What you want (servers, databases, etc.)
* How they should be configured

Terraform then:

1. Reads your files
2. Compares with real infrastructure
3. Creates/updates/deletes resources automatically.
