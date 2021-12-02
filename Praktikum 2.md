# Adminitration System Practical Reports 2
Muhammad Rafi Irzam (1202190063) & Galih Dimas Prastowo (1202190018)
## Practical Question
https://github.com/aldonesia/Sistem-Administrasi-Server-2021/blob/master/modul-2/soal_praktikum.md
## 1.
### Destroy lxc_landing ver 18 and install ubuntu landing ver 20 (focal)
```bash
sudo lxc-destroy ubuntu_landing
```
<img width="594" alt="2" src="https://user-images.githubusercontent.com/83237598/144440310-03467ad1-af56-42c7-bfbe-32875efe8913.png">

```bash
sudo lxc-create -n ubuntu_landing -t download -- --dist ubuntu --release focal --arch amd64 --force-cache --no-validate --server images.linuxcontainers.org
```
### Config IP ubuntu landing (10.0.3.103)
```bash
sudo lxc-start -n ubuntu_landing
sudo lxc-attach  -n ubuntu_landing
nano /etc/netplan/10-lxc.yaml
netplan apply
```
<img width="547" alt="3 (2)" src="https://user-images.githubusercontent.com/83237598/144442747-31dad820-a909-4bf3-9812-f161b21d81e2.png">


![image](https://user-images.githubusercontent.com/83237598/144441576-6e805588-8591-4c79-8e5d-a00a27dcecbb.png)

<img width="467" alt="5" src="https://user-images.githubusercontent.com/83237598/144442904-d01defea-6634-41bc-b7c7-04ad4cbed890.png">

### Set auto start at Ubuntu_landing
<img width="580" alt="6" src="https://user-images.githubusercontent.com/83237598/144443943-9660f07e-3089-4f1a-89b4-fb5b8d219599.png">

### Instal SSH
<img width="475" alt="7" src="https://user-images.githubusercontent.com/83237598/144444483-0c9c4a7f-bdb9-4eb1-914c-95e1c2d81ec4.png">

### Set PermitRootLogin yes & RSAAuthentication yes
![image](https://user-images.githubusercontent.com/83237598/144445223-e7f114aa-2b2a-4a59-a42b-ed1b5c703dce.png)

### Check ssh, it's already run or not
<img width="604" alt="8" src="https://user-images.githubusercontent.com/83237598/144445384-89f4b0bb-cf88-47c5-83ff-4db09a8f11af.png">

## 2.
### Same step as ubuntu landing
### Destroy lxc_landing ver 18 and install ubuntu landing ver 20 (focal)
<img width="559" alt="no 2" src="https://user-images.githubusercontent.com/83237598/144446528-993ea3bc-26cb-4fc7-ab54-cd5e9bd817ce.png">

## 3.
## vm.local/
### Install Laravel with ansible & go to ansible directory and create new folder

![image](https://user-images.githubusercontent.com/83237598/144457459-47704029-43ec-4a9b-ad7c-1ef6e9dc1868.png)
  
### create host
  
![image](https://user-images.githubusercontent.com/83237598/144457532-1794e9ba-4c92-4517-b749-7ea1a6eebaaf.png)

  ```markdown
  [landing]
  ubuntu_landing ansible_host=lxc_landing.dev ansible_ssh_user=root ansible_become_pass=sepasi
  
  ```

 ### create directory to run php folder
          	
![image](https://user-images.githubusercontent.com/83237598/144458602-c788dac3-b757-4bc5-ad26-b23fc83e2f88.png)
    

  ```
  ---
  - hosts: all
    become : yes
    tasks:
      - name: install nginx nginx extras
        apt:
         pkg:
           - nginx
           - nginx-extras
         state: latest
      - name: start nginx
        service:
         name: nginx
         state: started
      - name: menginstall tools
        apt:
         pkg:
           - curl
           - software-properties-common
           - unzip
         state: latest
      - name: "Repo PHP 7.4"
        apt_repository:
          repo="ppa:ondrej/php"
      - name: "Updating the repo"
        apt: update_cache=yes
      - name: Installation PHP 7.4
        apt: name=php7.4 state=present
      - name: install php untuk laravel
        apt:
         pkg:
            - php7.4-fpm
            - php7.4-mysql
            - php7.4-mbstring
            - php7.4-xml
            - php7.4-bcmath
            - php7.4-json
            - php7.4-zip
            - php7.4-common
         state: present
  ```

  

  ### create folder installcomposer.yml

  ![image](https://user-images.githubusercontent.com/83237598/144459972-36237625-d760-4ccc-af8f-94925f15a39a.png)


    


  ```
  ---
   -hosts: all
    become : yes
    tasks:
     - name: Download and install Composer
       shell: curl -sS https://getcomposer.org/installer | php
       args:
        chdir: /usr/src/
        creates: /usr/local/bin/composer
        warn: false
     - name: Add Composer to global path
       copy:
        dest: /usr/local/bin/composer
        group: root
        mode: '0755'
        owner: root
        src: /usr/src/composer.phar
        remote_src: yes
     - name: Composer create project
       become_user: root
       composer:
        command: create-project
        arguments: laravel/laravel landing 
        working_dir: /var/www/html
        prefer_dist: yes
       environment:
          COMPOSER_NO_INTERACTION: "1"
     - name: mengkopi file .env.example jadi .env
       copy:
        dest: /var/www/html/landing/.env.example
        src: /var/www/html/landing/.env
        remote_src: yes
     - name: mengganti konfigurasi .env
       lineinfile:
        path: /var/www/html/landing/.env
        regexp: "{{ item.regexp }}"
        line: "{{ item.line }}"
        backrefs: yes
       loop:
        - { regexp: '^(.*)DB_HOST(.*)$', line: 'DB_HOST=10.0.3.200' }
        - { regexp: '^(.*)DB_DATABASE(.*)$', line: 'DB_DATABASE=landing' }
        - { regexp: '^(.*)DB_USERNAME(.*)$', line: 'DB_USERNAME=admin' }
        - { regexp: '^(.*)DB_PASSWORD(.*)$', line: 'DB_PASSWORD= ' }
        - { regexp: '^(.*)APP_URL(.*)$', line: 'APP_URL=http://vm.local' }
        - { regexp: '^(.*)APP_NAME=(.*)$', line: 'APP_NAME=landing' }
     - name: Composer install ke landing
       composer:
         command: install
         working_dir: /var/www/html/landing
       environment:
         COMPOSER_NO_INTERACTION: "1"
     - name: generate php artisan
       args:
        chdir: /var/www/html/landing
       shell: php artisan key:generate
     - name: mengganti permission storage
       file:
        path: /var/www/html/landing/storage
        mode: 0777
        recurse: yes
  
  ```

  

  

  ### Install
  
  <img src= "https://github.com/acid99/Sistem-Administrasi-Server/blob/main/assets/laprak2/no%203/2021-11-30_6.png?raw=true">


  ### Create lxc_landing.dev

       ![22](https://user-images.githubusercontent.com/61863147/144443067-3965ad39-c88f-4250-9035-0f9763871e9c.PNG)


    ```
    server {
            listen 80;
    
            root /var/www/html/landing/public;
            index index.php index.html index.htm;
            server_name lxc_landing.dev;
    
            error_log /var/log/nginx/landing_error.log;
            access_log /var/log/nginx/landing_access.log;
    
            client_max_body_size 100M;
            location / {
                    try_files $uri $uri/ /index.php$args;
            }
            location ~\.php$ {
                    include snippets/fastcgi-php.conf;
                    fastcgi_pass unix:run/php/php7.4-fpm.sock;
                    fastcgi_param SCRIPTFILENAME $document_root$fastcgi_script_name;
            }
    }
    ```

    

  ### Create file config.yml

  ![image](https://user-images.githubusercontent.com/83237598/144459347-de209817-9aee-41eb-ac22-49f25a31c225.png)

    

    ```
    ---
    - hosts: all
      become : yes
      vars:
        domain: 'lxc_landing.dev'
      tasks:
       - name: stop apache2
         service:
          name: apache2
          state: stopped
          enabled: no
       - name: Write {{ domain }} to /etc/hosts
         lineinfile:
          dest: /etc/hosts
          regexp: '.*{{ domain }}$'
          line: "127.0.0.1 {{ domain }}"
          state: present
       - name: ensure nginx is at the latest version
         apt: name=nginx state=latest
       - name: start nginx
         service:
          name: nginx
          state: started
       - name: copy the nginx config file 
         copy:
          src: ~/ansible/laravel/lxc_landing.dev
          dest: /etc/nginx/sites-available/lxc_landing.dev
       - name: Symlink lxc_landing.dev
         command: ln -sfn /etc/nginx/sites-available/lxc_landing.dev /etc/nginx/sites-enabled/lxc_landing.dev
         args:
          warn: false
       - name: restart nginx
         service:
          name: nginx
          state: restarted
       - name: restart php7
         service:
          name: php7.4-fpm
          state: restarted
       - name: curl web
         command: curl -i http://lxc_landing.dev
         args:
          warn: false
    ```

    

  ### Install

![image](https://user-images.githubusercontent.com/83237598/144459478-9b735d1a-927f-4bb6-a7ec-8198fb2d2ae6.png)


  ### Open vm.local/

  ![image](https://user-images.githubusercontent.com/83237598/144459187-adbc0d6a-c6b3-403d-8279-9c887f9e5277.png)

## 4.      
