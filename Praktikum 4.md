# Adminitration System Practical Reports 4
Muhammad Rafi Irzam (1202190063) & Galih Dimas Prastowo (1202190018)
## Practical Question
https://github.com/aldonesia/Sistem-Administrasi-Server-2021/blob/master/modul-4/silabus.md
### - Duplicate 2 containers then start
![image](https://user-images.githubusercontent.com/83237598/148384091-aeba656e-bcee-412a-b976-3ea31a1b4b67.png)
### - Change IP address ubuntu_php.7.4_2 to 10.0.3.111/24 & ubuntu_php.7.4_3 to 10.0.3.121
![image](https://user-images.githubusercontent.com/83237598/148384692-67b8128e-f77f-4f23-a89e-03aadcf0cefb.png)
### - Go to lxc_php7_2.dev hosts directory and change server name
![image](https://user-images.githubusercontent.com/83237598/148385021-bf901cb8-bf1d-4254-875d-82ce7309e7e9.png)
![image](https://user-images.githubusercontent.com/83237598/148385181-5aaa0ae0-027b-49ff-bfe5-326eebab5b67.png)
### - restart nginx
![image](https://user-images.githubusercontent.com/83237598/148385402-60bf1d82-360e-447a-8e31-600c4c605366.png)
### - Do the same step for ubuntu_php7.4_3 (10.0.3.121), debian_php5.6_2 (10.0.3.112), and debian_php5.6_3 (10.0.3.122)
### - Go to directory hosts on vm and add server name
![image](https://user-images.githubusercontent.com/83237598/148385721-35de26a6-ed04-4555-81fc-81c37bde4d6e.png)
### - Run the JMeter

### - After that, go to nano /etc/nginx/sites-available/vm.local then add upstream
![image](https://user-images.githubusercontent.com/83237598/148386361-40df0f27-2966-4b2b-9804-818ddc487845.png)
### - Change the proxy_pass
![image](https://user-images.githubusercontent.com/83237598/148386483-c4f1dafb-5e93-42a4-b79b-adb59d4211a8.png)
### - Back to JMeter

## Analysis Results
