layout: post
title:  Oracle Cloud SSH Key Pair
date:   2024-01-22
image:  
tags:   [oracle, oci]
---
# Create an SSH Key for Oracle Cloud VMware Solution

Oracle Cloud Infrastructure (OCI) provides a robust and secure cloud computing environment for businesses and developers. One essential aspect of securing your Oracle Cloud VMware Solution is managing SSH keys. In this blog, we'll guide you through the process of creating an SSH key and associating it with your ESXi Hosts.

## Why SSH Keys?

SSH keys play a crucial role in securing communication between your local machine and OCI instances. They provide a secure way of connecting to your compute instances without the need for passwords. By using SSH keys, you enhance the security of your infrastructure and simplify access management.

1. **Login to OCI Console:**
   - Open your web browser and go to the [OCI Console](https://cloud.oracle.com/).
   - Log in with your credentials.

2. **Navigate to Compute Instances:**
   - In the OCI Console, navigate to the "Compute" service.

3. **Launch a New Compute Instance:**
   - Click on "Instances" in the left-hand navigation menu.
   - Click the "Create Instance" button to launch a new compute instance.

4. **Add SSH Keys:**
   - In the "Create Compute Instance" form, scroll down to the "Add SSH Keys" section.
   - Click on the "Generate a key pair for me" option.

5. **Review Key Pair Details:**
   - The console will generate a new SSH key pair for you.

6. **Save SSH Keys:**
   - Click on the "Save private Key" button
   - Click on the "Save public Key" button

7. **Oracle Cloud VMware Solution:**
   - You are now ready to deploy Oracle Cloud VMware Solution!
