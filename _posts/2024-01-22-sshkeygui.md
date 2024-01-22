1. **Login to OCI Console:**
   - Open your web browser and go to the [OCI Console](https://cloud.oracle.com/).
   - Log in with your credentials.

2. **Navigate to Compute Instances:**
   - In the OCI Console, navigate to the "Compute" service.

3. **Launch a New Compute Instance:**
   - Click on "Instances" in the left-hand navigation menu.
   - Click the "Create Instance" button to launch a new compute instance.

4. **Configure Compute Instance:**
   - Fill in the required details for your new compute instance, such as the compartment, display name, availability domain, etc.

5. **Add SSH Key:**
   - In the "Create Compute Instance" form, scroll down to the "SSH Key" section.
   - Click on the "Generate a key pair for me" option.

6. **Review Key Pair Details:**
   - The console will generate a new SSH key pair for you.
   - Review the details, such as the key name and type.

7. **Save SSH Key:**
   - Click on the "Save SSH Key" button to associate the generated key pair with the new compute instance.

8. **Review and Create:**
   - Complete any other necessary configurations for your new compute instance.
   - Click on the "Next" button until you reach the "Review" step.
   - Review your configurations, and if everything looks good, click on the "Create" button.

9. **Connect to the New Instance:**
   - Once the new compute instance is created, you can connect to it using an SSH client.
   ```bash
   ssh -i <path_to_private_key_file> opc@<new_instance_public_ip>
