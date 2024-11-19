
### Step 1: Introduction to Idempotence
 Idempotence ensures that applying the same configuration multiple times doesn’t alter the environment after the first execution, avoiding unintended changes. Without idempotence, repeated runs of the same tasks could lead to inconsistencies, which is especially risky in production.

### Step 2: Set Up the Environment
1. **Install Ansible** on our virtual environment (WSL2)
   ```bash
   sudo apt update
   sudo apt install ansible -y
   ```


1. **Deploy a test host** as a container using Docker. We started an Ubuntu container that Ansible can manage:
   ```bash
   docker run -d --name ansible-test -p 2222:22 -e TZ=Europe/London -it ubuntu:latest
   ```
   ![](Ansible%20&%20Idempotency-1.png)

### Step 3: Write and Execute an Idempotent Playbook
We create this basic Ansible playbook to install Nginx (which serves as a great example for showing idempotence)

1. **Create a new playbook** file `first_playbook.yml`:
   ```yaml
   - name: Ensure Nginx is installed
     hosts: localhost
     tasks:
       - name: Install Nginx
         apt:
           name: nginx
           state: present
         become: yes
   ```
   ![](Ansible%20&%20Idempotency-3.png)

2. **Run the Playbook**
   ```bash
   ansible-playbook first_playbook.yml
   ```
   - The first run installs Nginx, showing that changes were made.
   ![](Ansible%20&%20Idempotency-2.png)
   - Running it again should indicate "ok" (no changes), as Ansible recognizes Nginx is already installed, showing idempotence.
   ![](Ansible%20&%20Idempotency-4.png)

### Step 4: Practical Exercise – Modify a Configuration File
Let’s add a task to create or update a configuration file, ensuring it’s applied only if needed.

1. **Extend the Playbook** to create a basic Nginx index file:
   ```yaml
   - name: Ensure Nginx is installed
     hosts: localhost
     tasks:
       - name: Install Nginx
         apt:
           name: nginx
           state: present
         become: yes

       - name: Set up index.html
         copy:
           dest: /var/www/html/index.html
           content: "<h1>TP1 Deploiment</h1>"
           owner: www-data
           group: www-data
           mode: '0644'
   ```
   ![](Ansible%20&%20Idempotency-5.png)

2. **Run the Playbook Again**
   - Ansible should show "changed" only for the initial run of the copy task if `/var/www/html/index.html` didn’t already exist. 
   ![](Ansible%20&%20Idempotency-6.png)
   - If we run it again, Ansible will recognize the file is as expected and mark the task as "ok."
   ![](Ansible%20&%20Idempotency-7.png)

### Step 5: Testing and Validating Idempotence
1. **Make a Change** to the environment by manually deleting or altering `index.html`:
   ```bash
   sudo rm /var/www/html/index.html
   ```
   
2. **Run the Playbook Again**
   - Ansible will recreate `index.html`, showing that it can bring the environment back to the expected state. This demonstrates how idempotence works when changes are made outside of Ansible.
   ![](Ansible%20&%20Idempotency-8.png)

### Step 6: Reflection and Conclusion

Understanding idempotence will help us avoid redundant operations, prevent configuration drift, and maintain system reliability as we build more complex automation tasks.
By applying idempotent principles, we’re better equipped to develop robust, scalable, and maintainable automation workflows—valuable skills for a DevOps engineer.
#### 1. **Key Observations on Idempotence in Ansible**
 We learned that Ansible ensures that tasks result in a consistent system state regardless of how many times they are run. For example, when installing `nginx` using the `apt` module with `state: present`, Ansible checks if `nginx` is already installed. On the first run, it installs `nginx` (showing "changed"), but on subsequent runs, it detects `nginx` is already present, so no action is needed (showing "ok").
#### 2. **Challenges in Ensuring Idempotence**

- **Dynamic Data**: Tasks with dynamic values (e.g., writing the current date and time to a file) may always show as “changed” due to the changing input data. This reveals a limitation of idempotence in tasks where conditions are expected to vary.
- **External Dependencies**: We saw that environment-dependent tasks, like those involving network configurations or external services, may show unexpected results if those dependencies change unexpectedly. Idempotence in such cases requires careful handling of task conditions.


---
**Work done by: Mohamed Aziz Bellaaj, Louay Badri, Salma Ghabri**