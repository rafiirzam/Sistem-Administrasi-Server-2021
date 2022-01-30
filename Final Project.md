# Adminitration System Practical Final Project
Muhammad Rafi Irzam (1202190063) & Galih Dimas Prastowo (1202190018)
## Final Project Questions
https://github.com/aldonesia/Sistem-Administrasi-Server-2021/tree/master/Final%20Project
### Architecture
![image](https://user-images.githubusercontent.com/83237598/151696346-4d8c1608-2efa-4b5b-b5ad-7b10003544a8.png)

### Create LXC in accordance to architecture
![image](https://user-images.githubusercontent.com/83237598/151695009-e651b52f-c453-4463-b6d1-bb4108697698.png)
![image](https://user-images.githubusercontent.com/83237598/151695025-3e704e6c-351f-47ce-b67a-347808263009.png)

### List of container and IP address
![Screenshot (522)](https://user-images.githubusercontent.com/83237598/151695047-99086f19-442e-4bc7-87b4-1b83ecac42e2.png)

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

### yii configuration with Ansible
- Create and config install-laravel.yml & directory
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
ansible-playbook -i hosts install-wp.yml -k
```

### mariaDB configuration with Ansible
- Create and config install-mariadb.yml & directory
![Screenshot (536)](https://user-images.githubusercontent.com/83237598/151706851-caf6e038-4f3e-4ade-af43-abd566967254.png)

- roles/db/tasks **(left)** & roles/db/templates/my.cnf **(right)**
![Screenshot (537)](https://user-images.githubusercontent.com/83237598/151707053-dc6e8682-3efb-4280-94a3-e8d8981a54c5.png)

- 

### Codeigniter configuration with Ansible
- Create and configuration install-ci.yml & directory

## Analysis Performance
1. Average throughputs

2. Average users

3. 
