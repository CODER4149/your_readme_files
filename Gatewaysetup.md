**Gateway Setup Document**
--------------------------------------------------------------------
**Commands**
---------------------------------------------------------------------
 mkdir test 
 
 ls 
 
 cd test/
 
 git clone 
 
 ls
 
 git clone https://github.com/iam-rnd/tagid-trial-theft-identity.git
 
 ls
 
 cd tagid-trial-theft-identity/
 
 ls
 
 git checkout 1-create-pos-selling-api 
 
 ls
 
 python3 -m venv venv
 
 ls
 
 cat requirements.txt 
 
 ls
 
 pip3 install -r requirements.txt 
 
 source venv/bin/activate
 
 pip3 install -r requirements.txt 
 
 ls
 
 sudo cp trial_theft_identity.servic /etc/systemd/system/
 
 sudo systemctl enable trial_theft_identity.service 
 
 sudo systemctl start trial_theft_identity.service 
 
 journalctl -u trial_theft_identity.service -f
 
 nano trial_theft_identity.service 
 
 pwd
 
 nano trial_theft_identity.service - If Requred to cahnge the path of servece file 
 
 cat trial_theft_identity.service -
 
 sudo cp trial_theft_identity.service /etc/systemd/system/
 
 sudo apt-get update && apt-get install libpq5 -y
 
 sudo systemctl enable trial_theft_identity.service 
 
 sudo systemctl start trial_theft_identity.service 
 
 journalctl -u trial_theft_identity.service -f
 
 ls
 
 nano config.json 
 
 sudo systemctl restart trial_theft_identity.service 
 
 journalctl -u trial_theft_identity.service -f
 
 history

---------------------------------------------------------

**service sample file**

# Reference
# https://github.com/torfsen/python-systemd-tutorial

[Unit]
Description=Trial Theft Identity

[Service]
# Command to execute when the service is started
User=pi

Group=pi

WorkingDirectory=home/pi/tagid-trial-theft-identity

ExecStart=/home/pi/tagid-trial-theft-identity/venv/bin/python3  /home/pi/tagid-trial-theft-identity/main.py

Environment="INSTALL_PATH=/home/pi/iam-gateway"

[Install]

WantedBy=default.target

---------this file extension is .service --------------


**Taking Remote Debugger**

---------------------- Start gateway side command------------------

 mkdir amolsir_testing
 
 cd amolsir_testing/
 
 python3 -m venv venv
 
 source venv/bin/activate
 
 pip3 install -r requirements.txt 
 
 history
 
 --------------- Start pycharm side connect debugger -------------------
 
 
 1. First be sure delete venv from your project while setup venv
 2. ![Screenshot from 2023-02-09 12-28-17](https://user-images.githubusercontent.com/68800883/217740369-776dd5df-103a-42a6-aaa9-b65698abbd9a.png)
 3. click on on_ssh
 4. enter your gateway ip, username, password
 5. on location choose which file you want to use choose python3
 6. click on create and rerun main.py

**Gateway net connection **
 curl -X POST http://:8090/login.xml --data-urlencode "mode=191" --data-urlencode "username=" --data-urlencode "password=" --data-urlencode "a=1633529001622" --data-urlencode "producttype=0"

