# Adminitration System Practical Final Project
Muhammad Rafi Irzam (1202190063) & Galih Dimas Prastowo (1202190018)
## Final Project Questions
https://github.com/aldonesia/Sistem-Administrasi-Server-2021/tree/master/Final%20Project
### Architecture
![image](https://user-images.githubusercontent.com/83237598/151696346-4d8c1608-2efa-4b5b-b5ad-7b10003544a8.png)

### Create LXC in accordance to architecture
- 6 LXC Ubuntu PHP 7.4
- 2 LXC Debian PHP 5.6
- 1 LXC Debian mariaDB server
![image](https://user-images.githubusercontent.com/83237598/151695009-e651b52f-c453-4463-b6d1-bb4108697698.png)
![image](https://user-images.githubusercontent.com/83237598/151695025-3e704e6c-351f-47ce-b67a-347808263009.png)

### Install Ansible
```bash
sudo apt install ansible sshpass
```

### Create directory
```bash
mkdir -p ~/ansible/tugas_akhir
```

### Create and setting hosts
![image](https://user-images.githubusercontent.com/83237598/152382016-d29fcffa-d2c0-4acf-9a76-c0564f0f454f.png)
![image](https://user-images.githubusercontent.com/83237598/152382030-0fccc732-c36c-4eb9-a053-32acda9407c3.png)

### Setting all of containers auto start
example:
```markdown
echo "lxc.start.auto = 1" >> /var/lib/lxc/lxc_db_server/config
```
### List of container and IP address
![Screenshot (522)](https://user-images.githubusercontent.com/83237598/151695047-99086f19-442e-4bc7-87b4-1b83ecac42e2.png)

- Configuration all lxc with command below

    - Install ssh server

    ```markdown
    apt install openssh-server
    ```

    - Adding configuration at /etc/ssh/sshd_config

    ```markdown
    nano /etc/ssh/sshd_config
    
    # setting config
    PermitRootLogin yes
    RSAAuthentication yes
    ```

    - Restart ssh server

    ```markdown
    service sshd restart
    ```

    - Setting password for all lxc

    ```markdown
    passwd (ex: 321)
    ```

    - Log out from all lxc

    ```markdown
    exit
    ```

    - Entering directory

    ```markdown
    cd ~/ansible/tugas_akhir
    ```

### Laravel Configuration with Ansible
- Create and config install-laravel.yml & directory
![Screenshot (523)](https://user-images.githubusercontent.com/83237598/151705298-99f00961-278e-4c6f-8ece-25797ce812ec.png)
- roles/lv/handlers **(left)** & roles/lv/tasks **(right)**
![Screenshot (525)](https://user-images.githubusercontent.com/83237598/151705612-e5e28666-9399-490d-bfde-fd10943d2978.png)

- roles/lv/templates (lv.conf, env.template, php7.conf)
![Screenshot (526)](https://user-images.githubusercontent.com/83237598/151705544-4be35c0c-fe64-409f-a305-51f9892bdfa0.png)
![Screenshot (527)](https://user-images.githubusercontent.com/83237598/151705846-27b701f1-fa55-41c0-bb4e-d68cfaa2a173.png)

- roles/php/handlers **(left)** & roles/php/tasks **(right)**
![Screenshot (524)](https://user-images.githubusercontent.com/83237598/151705984-2c109b15-14ec-4ae3-8734-1b3449d0181b.png)

- Run Ansible-Playbook
```bash
ansible-playbook -i hosts install-laravel.yml -k
```
![Screenshot (544)](https://user-images.githubusercontent.com/83237598/151730597-dbd7cac0-8484-4cf5-8a41-1024226dbc30.png)


### yii configuration with Ansible
- Create and config install-yii.yml & directory
```bash
mkdir -p roles/yii
mkdir -p roles/yii/handlers 
mkdir -p roles/yii/tasks
mkdir -p roles/yii/templates
```
- roles/yii/tasks **(left)** & roles/yii/handlers **(right)**
![Screenshot (529)](https://user-images.githubusercontent.com/83237598/151706438-4822d34b-ba74-40d6-818c-6bea65c05788.png)

- roles/yii/templates
![Screenshot (530)](https://user-images.githubusercontent.com/83237598/151706473-cc76f3ff-6c35-469c-b0a4-9eb5c93b59b7.png)

- Run Ansible-Playbook
```bash
ansible-playbook -i hosts install-yii.yml -k
```
![YII](https://user-images.githubusercontent.com/83237598/152486480-ccef408d-f001-44e4-b173-3fc969a01808.jpeg)


### Wordpress configuration with Ansible
- Create and config install-wordpress.yml & directory
![Screenshot (531)](https://user-images.githubusercontent.com/83237598/151706573-4e6506d5-84ed-4091-9610-fae06164e49b.png)

- roles/wp/tasks **(left)** & roles/wp/handlers **(right)**
![Screenshot (532)](https://user-images.githubusercontent.com/83237598/151706602-d87331fa-174d-4201-abc8-88df580fdb0c.png)

- roles/wp/templates (wp.conf, wordpress.conf, php7.conf)
![Screenshot (533)](https://user-images.githubusercontent.com/83237598/151706655-bc653925-119f-455d-90d5-bc1d3bcbfa17.png)
![Screenshot (534)](https://user-images.githubusercontent.com/83237598/151706668-a69fd5c8-685a-4116-96a1-1d2124555908.png)

- Run Ansible-Playbook
```bash
ansible-playbook -i hosts install-wordpress.yml -k
```

### mariaDB configuration with Ansible
- Create and config install-mariadb.yml & directory
![Screenshot (536)](https://user-images.githubusercontent.com/83237598/151706851-caf6e038-4f3e-4ade-af43-abd566967254.png)

- roles/db/tasks **(left)** & roles/db/templates/my.cnf **(right)**
![Screenshot (537)](https://user-images.githubusercontent.com/83237598/151707053-dc6e8682-3efb-4280-94a3-e8d8981a54c5.png)

- roles/db/handlers
![Screenshot (538)](https://user-images.githubusercontent.com/83237598/151730238-bc1fe268-4d73-4507-b6b3-d87a9bcaa306.png)

- roles/pma/tasks **(left)** & roles/pma/templates/pma.local **(right)**
![Screenshot (539)](https://user-images.githubusercontent.com/83237598/151730306-1046d17e-3ef3-4025-b007-d88fc4575c4f.png)

- Run Ansible-Playbook
```bash
ansible-playbook -i hosts install-mariadb.yml -k
```

### Codeigniter configuration with Ansible
- Create and configuration install-ci.yml & directory
![Screenshot (541)](https://user-images.githubusercontent.com/83237598/151730166-2c8aee28-dfa8-4779-80ff-51096e51a30b.png)

- roles/ci/tasks **(left)** & roles/ci/handlers **(right)**
![Screenshot (542)](https://user-images.githubusercontent.com/83237598/151730526-7a94debe-31cd-456f-802d-297c71a542ea.png)

- roles/ci/templates/ci.conf
![Screenshot (543)](https://user-images.githubusercontent.com/83237598/151730558-3f9268d1-755f-496f-8db3-35503dfc1a53.png)

- Run Ansible-Playbook
```bash
ansible-playbook -i hosts install-ci.yml -k
```
![ci](https://user-images.githubusercontent.com/83237598/152486142-2cf01a9c-2ac2-4c56-91be-29f2ed1ad382.jpeg)

## Hasil
### YII
![Screenshot (245)](https://user-images.githubusercontent.com/83237598/152382984-47847779-9f5a-4fa4-8e60-312384183136.png)

### Codeigniter
![Screenshot (246)](https://user-images.githubusercontent.com/83237598/152383141-244a253c-b449-4100-b678-5bf8f74fa1dd.png)

### Wordpress
![Screenshot (247)](https://user-images.githubusercontent.com/83237598/152383499-d8eda54a-2a77-4ce5-8cba-1dd08053a4b5.png)

### Phpmyadmin
![Screenshot (248)](https://user-images.githubusercontent.com/83237598/152383874-7fb8631c-20a2-4bbc-b9a1-f904a0a3500d.png)

### Laravel
![Screenshot (249)](https://user-images.githubusercontent.com/83237598/152384171-8634ed97-9be0-4cb1-8b9e-c261ecd053e3.png)
