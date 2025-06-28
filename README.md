<!-- Cloud Foundation / Landing Zone Setup Guide for Google Cloud Platform (GCP) -->

<h1 align="center">☁️ Google Cloud Foundation & Landing Zone Setup Guide 🚀</h1>

<p align="center">
  <img src="https://cloud.google.com/images/social-icon-google-cloud-1200-630.png" width="200" alt="Google Cloud Logo" />
</p>

## Table of Contents 📑

- [Introduction](#introduction)
- [Manual Setup Process](#manual-setup-process)
  - [Organization Setup](#organization-setup)
  - [User and Group Configuration](#user-and-group-configuration)
  - [Billing Account Setup](#billing-account-setup)
  - [Hierarchy and Access Management](#hierarchy-and-access-management)
  - [Security](#security)
  - [Networking with Shared VPC](#networking-with-shared-vpc)
  - [Terraform Configuration and Deployment](#terraform-configuration-and-deployment)
  - [Folder and Project Customization](#folder-and-project-customization)
  - [Additional Points to Note](#additional-points-to-note)
- [Automated Setup Using Terraform Example Foundation Repository](#automated-setup-using-terraform-example-foundation-repository)
  - [Stages of the Repository](#stages-of-the-repository)
  - [Customizing the Repository](#customizing-the-repository)
  - [Example Directory Structure After Customization](#example-directory-structure-after-customization)
- [Conclusion](#conclusion)
- [Contributing](#contributing)
- [License](#license)

## Introduction 🌟

A landing zone, also referred to as a cloud foundation, is a modular, scalable, and secure framework that enables organizations to adopt Google Cloud efficiently and in alignment with their business needs. It establishes a standardized baseline for deploying enterprise workloads, ensuring compliance, security, and operational best practices.

This guide provides two approaches to setting up a landing zone in Google Cloud:
1. **Manual setup** through the Google Cloud Console
2. **Automated setup** using the Terraform Example Foundation Repository

## Manual Setup Process 🖥️

### Organization Setup 🏢

To initiate the creation of a landing zone in Google Cloud, follow these steps:

1. Navigate to IAM > Identity and Organization in the Google Cloud Console
2. Review the checklist under Setup Production to ensure prerequisites are met
3. Progress through the checklist to configure a robust and scalable landing zone

Choose one of the following options based on your current setup:

- **I'm a new customer**: You'll set up Cloud Identity, verify your domain, and create your organization
- **I'm a current Workspace customer**: You can optionally enable Cloud Identity
- **I'm a current Cloud Identity customer**: You'll review that Cloud Identity is enabled for your organization

<details>
<summary>Google Workspace Integration</summary>

Google Workspace seamlessly integrates with your organization's domain and billing account, providing a unified platform for productivity and identity management. A 14-day free trial is available to help organizations evaluate its features.

**Key Features:**
- Productivity tools: Docs, Sheets, Slides, and more
- Secure communication: Gmail, Google Meet, and Chat
- Centralized user management for Google Cloud and other applications
</details>

<details>
<summary>Cloud Identity</summary>

Cloud Identity is a standalone identity and access management service that complements Google Workspace. It offers basic and premium tiers, with the free tier sufficient for most organizations.

**To access:** Billing account >> Subscriptions >> Cloud Identity

**Key Features:**
- Unified management of users and devices
- Single Sign-On (SSO) for seamless access to applications
- Enhanced security features, such as multi-factor authentication (MFA)
</details>

### User and Group Configuration 👥

After establishing the organization, the next step is to configure users and groups:

1. **Create Users**: 
   - Add users to Google Workspace to enable access to resources
   - Use the option "Add to the group" to add users to groups

2. **Groups Setup**: 
   - Select predefined groups manually or use the "Create All" option to generate all groups at once
   - Assign users to each group (at least two users are required for IAM setup)

3. **Administrative Access Configuration**:
   - Google provides predefined roles for groups
   - Add or edit roles and assign them to users as needed

### Billing Account Setup 💰

Configure a billing account to fund projects within the landing zone:

- Set up a payment profile and link it to multiple projects
- Monitor and manage billing quotas proactively to avoid disruptions
- Apply for quota increases as necessary via the quota management page

### Hierarchy and Access Management 🗂️

The Google Cloud resource hierarchy organizes your cloud resources and maps them to your organization. It includes:

- **Organization Resource**: The top-level resource in Google Cloud
- **Folders and Projects**: Logical containers for resources

**Configure Your Recommended Hierarchy:**

<table>
  <tr>
    <th>Hierarchy Type</th>
    <th>Description</th>
    <th>Best For</th>
  </tr>
  <tr>
    <td>Simple, Environment-Oriented</td>
    <td>Projects organized by environment type</td>
    <td>Development, testing, and production environments</td>
  </tr>
  <tr>
    <td>Simple, Team-Oriented</td>
    <td>Projects grouped by team responsibilities</td>
    <td>Small teams working on specific tasks</td>
  </tr>
  <tr>
    <td>Environment-Oriented</td>
    <td>Separating environments (e.g., dev, stage, prod)</td>
    <td>Better control over environment-specific resources</td>
  </tr>
  <tr>
    <td>Business Unit-Oriented</td>
    <td>Projects aligned with specific business units or departments</td>
    <td>Large organizations managing cross-departmental resources</td>
  </tr>
</table>

This hierarchy helps define access management policies (IAM) and organization policies.

### Security 🔒

#### Security Command Center (SCC)

The Security Command Center is a centralized tool for identifying vulnerabilities and managing security risks.

**Service Tiers:**
- **Standard Tier**: Free with basic security features
- **Premium Tier**: Paid version with advanced features, such as container threat detection and DDoS protection

> 💡 **Tip**: Activate the Standard tier to initiate security scans and identify potential vulnerabilities.

#### Centralized Logging and Monitoring 📊

Google Cloud's centralized logging and monitoring services (via Cloud Logging and Cloud Monitoring) provide actionable insights:

- Simplify debugging with detailed logs
- Monitor resource utilization and system health
- Set up alerts for critical events

### Networking with Shared VPC 🌐

Shared VPC enables centralized and secure networking across multiple projects within an organization:

- Allows resources in different projects to communicate securely using internal IPs
- Simplifies network management by consolidating networking resources into a single host project

**Components:**
- **Host Project**: Configures subnet ranges, firewall rules, and network regions
- **Service Projects**: Connect to the host project for shared access to networking resources

**VPC Configuration Options:**

1. **Custom VPC**: Dedicated VPC per project for isolated environments
2. **Shared VPC**: Centralized VPC shared across projects, recommended for enterprise setups
3. **VPC Peering**: Direct connection between two VPCs, less preferred for large-scale setups

### Terraform Configuration and Deployment ⚙️

Google Cloud provides comprehensive Terraform templates to automate landing zone deployment. These templates include configurations for networking, IAM, monitoring, and more.

1. **Download Terraform Folder**:
   - Provides a folder containing configurations for setup

2. **Direct Deployment**:
   - Deploy resources directly via Terraform

**Terraform State File:**
- Create a bucket for the Terraform state file and specify the region
- Optionally, unselect items from the checklist to exclude them from deployment

**Sample Terraform Directory Structure:**

```
terraform/
├── main.tf
├── variables.tf
├── outputs.tf
├── backend.tf
└── modules/
    ├── iam/
    ├── networking/
    ├── logging/
    └── monitoring/
```

#### Terraform Deployment Steps

1. Install gcloud and Terraform using their respective installation links

2. Authenticate user:
   ```bash
   gcloud auth login
   gcloud auth application-default login
   ```

3. Set project and quota:
   ```bash
   gcloud config set project PROJECT_ID
   gcloud services enable cloudresourcemanager.googleapis.com
   ```

4. Initialize, plan, and apply the deployment:
   ```bash
   terraform init
   terraform plan -out=plan.out
   terraform apply plan.out
   ```

5. Deploy specific resources (e.g., VMs):
   ```bash
   terraform apply -target=module.compute
   ```

### Folder and Project Customization 🛠️

As per company requirements, customize the Terraform configuration:

- Instead of having two projects in each folder, limit it to one project per folder. This simplifies management and aligns with organizational needs.

**Network Customization:**

For small organizations, instead of utilizing shared VPC and hybrid networking (which may be complex), consider deploying custom VPCs for each project if required. Custom VPCs offer isolation and simplicity for smaller setups.

**Workload Deployment:**

Based on the organizational requirements:

- Fully customize resources post-landing zone setup
- Alternatively, use predefined workloads provided by GCP for rapid deployment

> ⚠️ **Important**: After validate and plan, verify all resources before applying.

### Additional Points to Note ⚠️

- **Quota Check**: Ensure sufficient project billing quota. If not, request an increase.
- **Troubleshooting**: Misconfigurations can be challenging to resolve. Destroying the setup may not fully revert changes due to lifecycle prevention policies and unique IDs. Update configurations cautiously.

## Automated Setup Using Terraform Example Foundation Repository 🤖

### Stages of the Repository 📚

The terraform-example-foundation repository provides a structured approach to setting up a secure Google Cloud foundation using Terraform. It follows the Google Cloud Enterprise Foundations Blueprint and is designed for large enterprise organizations.

The repository is divided into several stages, each representing a distinct Terraform project. These stages must be applied in sequence to build the foundation:

1. **0-bootstrap**: Bootstraps the Google Cloud organization, creating required resources and permissions
2. **1-org**: Sets up common resources such as Security Command Center notifications, KMS, and logging
3. **2-environments**: Creates shared projects for each environment (development, nonproduction, production)
4. **3-networks-dual-svpc**: Creates Shared VPCs for each environment with a standard configuration
5. **3-networks-hub-and-spoke**: Alternative to 3-networks-dual-svpc, using a hub-and-spoke network model
6. **4-projects**: Creates service projects attached to the Shared VPCs
7. **5-app-infra**: Deploys a simple Compute Engine instance in one of the business unit projects

### Customizing the Repository 🔧

#### General Customization

To customize the repository according to your organization's requirements, follow these steps:

- **Fork the Repository**: Start by forking the repository to your own version-control system
- **Update Variables**: Each stage contains a terraform.tfvars file where you can update variables to match your environment. Check the Inputs section of the README files for optional variables
- **Modify Terraform Code**: Adjust the Terraform code in each stage as needed. This may involve adding new resources, changing configurations, or integrating with other systems

#### Removing a Stage

To remove an existing stage, follow these steps:

1. **Delete the Directory**: Remove the directory corresponding to the stage
2. **Update Dependencies**: Ensure that any dependencies referencing the removed stage are updated or removed in other stages
3. **Update CI/CD Pipelines**: Modify CI/CD pipeline configurations to exclude references to the deleted stage

#### Adding a Custom Stage

To introduce a new custom stage, follow these steps:

1. **Create the Directory**: Add a new directory for the custom stage
2. **Write Terraform Code**: Implement Terraform configurations following the structure and conventions used in existing stages
3. **Update Dependencies**: If the new stage relies on outputs from other stages, ensure proper dependency management
4. **Update CI/CD Pipelines**: Integrate the new stage into CI/CD pipeline configurations to maintain the correct deployment sequence

### Example Directory Structure After Customization 📂

After making modifications, the directory structure might look like this:

```
/terraform-example-foundation/
├── 0-bootstrap/
├── 1-org/
├── 2-environments/
├── 3-networks/
├── 4-projects/
├── 5-app-infra/
└── custom-stage/
```

## Conclusion 🏁

Setting up a landing zone in Google Cloud provides a robust foundation for cloud adoption. Whether using the manual approach through the Google Cloud Console or the automated approach with the terraform-example-foundation repository, organizations can achieve a scalable, secure, and efficient cloud environment that supports enterprise workloads effectively.

By following the guidelines in this repository, you can establish a well-architected Google Cloud foundation that aligns with your organization's needs and best practices.

## Contributing 🤝

Contributions are welcome! Please feel free to submit a Pull Request.

## License 📄

This project is licensed under the MIT License - see the LICENSE file for details.
