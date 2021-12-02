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
