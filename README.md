#  HAProxy Reverse Proxy & Load Balancing Project



##  Overview

This project demonstrates the use of HAProxy as a reverse proxy and load balancer to route traffic based on domain name. It serves two React frontend applications running on separate virtual machines.

## I. Project Architecture with HAProxy as a Reverse Proxy
+ VM1: 192.168.232.110: (HAProxy - Reverse Proxy)

+ VM2: 192.168.232.111:3000 green-app.com React App

+ VM3: 192.168.232.113:3000 white-app.com React App


##  Setup Instructions
###  Step 1: Clone, install dependencies and run React apps on VM2 and VM3

```
git clone https://github.com/croyce97/HAproxy_project.git
sudo apt update -y
sudo apt install npm
```
* On VM2:
`sudo vi HAproxy_project/src/index.css`

In the .square { ... } block, replace line `background: var(--white);` with `background: var(--green);`.
```
cd ..
cd HAproxy_project
npm start
```

* On VM3:
```
cd HAproxy_project
npm start
```

+ Visit: http://192.168.232.111:3000

+ Visit: http://192.168.232.113:3000
###  Step 2: Install and configure HAProxy on VM1
```
sudo apt update
sudo apt install haproxy -y
sudo vi /etc/haproxy/haproxy.cfg
```
* Copy [haproxy_reverse_proxy.conf](https://github.com/croyce97/HAproxy_project/blob/main/haproxy_reverse_proxy.cfg) into this file.


### Step 3: Add local DNS mapping for `white-game.com` and `green-game.com`

Local Windows Machine: 
+ Open Notepad as Administrator
+ Open the file: `C:\Windows\System32\drivers\etc\hosts`
+ Add: `192.168.232.110    white-game.com green-game.com`

###  Step 4: Restart HAProxy on VM1 and access the apps
```
sudo systemctl restart haproxy
sudo systemctl enable haproxy
```
Visit: http://green-game.com [green-game.com](https://github.com/croyce97/HAproxy_project/blob/main/Images/green-game.com.jpeg)

Visit: http://white-game.com [white-game.com](https://github.com/croyce97/HAproxy_project/blob/main/Images/white-game.com.jpeg)

## II. Project Architecture with HAProxy as a Load Balancer
+ VM1: 192.168.232.110: canhnq.com (HAProxy - Load Balancer) 

+ VM2: 192.168.232.111:3000 React App

+ VM3: 192.168.232.113:3000 React App


##  Setup Instructions
###  Step 1: Clone, install dependencies and run React apps on VM2 and VM3

```
git clone https://github.com/croyce97/HAproxy_project.git
sudo apt update -y
sudo apt install npm
cd HAproxy_project
npm start
```

+ Visit: http://192.168.232.111:3000

+ Visit: http://192.168.232.113:3000
###  Step 2: Install and configure HAProxy on VM1
```
sudo apt update
sudo apt install haproxy -y
sudo vi /etc/haproxy/haproxy.cfg
```
* Copy [haproxy_load_balancing.conf](https://github.com/croyce97/HAproxy_project/blob/main/haproxy_load_balancing.cfg) into this file.


### Step 3: Add local DNS mapping for `canhnq.com`
VM1: 
+ `sudo vi /etc/hosts`
+ Add `127.0.0.1  canhnq.com`

Local Windows Machine: 
+ Open Notepad as Administrator
+ Open the file: `C:\Windows\System32\drivers\etc\hosts`
+ Add: `192.168.232.110    canhnq`


###  Step 4: Restart HAProxy on VM1 and access the apps
```
sudo systemctl restart haproxy
sudo systemctl enable haproxy
```
Visit: http://canhnq.com [canhnq.com](https://github.com/croyce97/HAproxy_project/blob/main/Images/canhnq.com.jpeg)

Visit: http://canhnq.com:8405/stats with username: `admin`, password:`admin123` to monitor. [canhnq.com:8405/stats](https://github.com/croyce97/HAproxy_project/blob/main/Images/LB-stats.jpeg)
