# Tutorial-yiimp-mining-pool-2022-2023-working
Tutorial yiimp 2022 working
###### Discord: https://discord.gg/K5KVvgm7v7
###### - If this tutorial helped you, make a contribution
###### BTC: 1Ljwbwd6Z2UDkscDroHdnave1hzmjApmCD
###### LTC: LeVPHyxkvGQ4fFW9DFGPYS6deNWY1AcSBo
###### DOGE: DE38DhPsxH8mub5XVhJZxFgKHMbUXhLEMp
###### ETH: 0x4da146cfd87bb6ede98bd7ef78791efc281dde3b

###### - Tutorial to help install yiimp
###### - Tutorial para ajudar na instalação do yiimp
###### - Pools that used this tutorial: https://onfirepool.ddns.net/

#### Follow the steps, and your yiimp will be operational


####   Requirements:
####   UBUNTU 18.04 (I used the minimal install)
----------------------------------------------------------------------------------------------------------------------------------------------------------------------
#### 1 - install git, curl, make, and gcc
```
sudo apt install git
sudo apt install curl
sudo apt install make
sudo apt update
sudo apt install build-essential
```
#### 1.2 - Use no-ip for domain (optional)
```
cd /usr/local/src/
sudo wget http://www.noip.com/client/linux/noip-duc-linux.tar.gz
sudo tar xf noip-duc-linux.tar.gz
cd noip-2.1.9-1/
sudo make install
```
1.2 - After the make install command, it will request your noip email and password, after that just choose your update options, and your noip is ready to go.

#### 2 - Download a reliable yiimp installer. I recommend using yiimp Dirty Harry (if you use another, replace the command below with the installer of your choice)
```
sudo curl https://raw.githubusercontent.com/DirtyHarryDev/Yiimp-Server-Installer/master/bootstrap.sh | bash
```
After running the command it will ask you to restart the machine, and give instructions on how to proceed with the installation after the restart, in my case I am using Dirty Harry, so the command will be yiimpserver

#### 3 - Setting up and installing yiimp
 > Select yiimp single server

 ![This is an image](https://media.discordapp.net/attachments/932109857698488330/945390426448330882/Screenshot_from_2022-02-21_15-23-07.png)
 
 #### I'm using domain so select the option to add to domain
 

> I'm not using subdomain

![This is an image](https://media.discordapp.net/attachments/932109857698488330/945390428549705749/subdomin.png)

> Fill in your domain

![This is an image](https://media.discordapp.net/attachments/932109857698488330/945390427161383022/dominio.png)

#### Your stratum will be the same domain but with stratum before


> Select to install the ssl certificate automatically, this will leave your site with the padlock indicating it is secure

![This is an image](https://media.discordapp.net/attachments/932109857698488330/945390428230930552/ssl.png)
![This is an image](https://files.tecnoblog.net/wp-content/uploads/2018/11/https-cadeado-seguranca-700x394.jpg)

#### Add an email address, so the pool will notify you about blocks


> Configure link to admin area

![This is an image](https://media.discordapp.net/attachments/932109857698488330/945390470492741723/adminportal.png)

> I leave auto exchange disabled in my pool, you can leave it enabled, it's up to you

![This is an image](https://media.discordapp.net/attachments/932109857698488330/945390426666463282/autoexchange.png)

> I leave the dedicated ports for the coins enabled, but it's up to your discretion

![This is an image](https://media.discordapp.net/attachments/932109857698488330/945390427404632064/portas.png)

> This part is very important so that you can access the admin panel of your pool - go to https://whatismyipaddress.com/ and put your ipv4 in the config

![This is an image](https://media.discordapp.net/attachments/932109857698488330/945390427723407390/publicip.png)

> Now configure your pool passwords, I recommend using the automatically generated ones (but remember to save them) or you can change them to one of your choice

![This is an image](https://media.discordapp.net/attachments/932109857698488330/945390427996033074/senha1.png)

> After that you will confirm your settings and give Yes to start the installation

![This is an image](https://media.discordapp.net/attachments/932109857698488330/945390426897137704/confirma.png)

> Installation can take many minutes

![This is an image](https://media.discordapp.net/attachments/932109857698488330/945392848839245824/insta.png)

> After the installation is finished it will give you the information to connect as admin in your pool, then save, and ask you to restart the machine - IT IS IMPORTANT THAT YOU RESTART FOR IT TO WORK

![This is an image](https://media.discordapp.net/attachments/932109857698488330/945393351979597864/Screenshot_from_2022-02-20_00-45-09.png?width=995&height=559)

### Ready now you have yiimp installed on your machine, congratulations, but don't go out releasing fireworks because it probably won't be working, as soon as you access your site it will present the white page of death
> This happens because of the PHP version that yiimp uses, ubuntu downloads the latest version not being compatible with the pool
# Now let's fix it
#### Let's install the right php
```
sudo apt install php7.3-memcache
sudo apt install php7.3-memcached
sudo apt install memcached
```
#### Now let's make the system switch from php 8.* to 7.3
```
sudo update-alternatives --config php
```
> select the option corresponding to PHP7.3

#### Now just restart nginx and php
```
sudo service nginx restart
sudo service php7.3-fpm restart
```
#### For you to add a port and start stratum automatically, just type the addport command in the terminal
> will ask for the currency symbol and the algorithm
> just fill in correctly that it will start alone

# Ready now your pool is almost 100%


#### If you install a coin BTC, LTC, DASH, among others, you will have to fix the coin_results.php (this solve RPC Error -8:label argument must be a valid label name or "*" )
> Using dirty harry as an example. go to /home/yiimp-data/yiimp/site/web/yaamp/modules/site/coin_resuts.php
>  look for
```
$account = '';
if ($DCR || $DGB) $account = '';
```
>and then below the other coins, add your coins
```
else if ($coin->symbol == "BTC") $account = ''; //ONFIRE TEST

else if ($coin->symbol == "DASH") $account = ''; //ONFIRE TEST

else if ($coin->symbol == "LTC") $account = ''; //ONFIRE TEST
```

example:
```
$account = '';
if ($DCR || $DGB) $account = '';

else if ($ETH) $account = $coin->master_wallet;

else if ($coin->symbol == "RNG") $account = '';

else if ($coin->symbol == "ZENX") $account = '';

else if ($coin->symbol == "BTC") $account = ''; //TESTE ONFIRE

else if ($coin->symbol == "DASH") $account = ''; //TESTE ONFIRE

else if ($coin->symbol == "LTC") $account = ''; //TESTE ONFIRE
```
# Congratulations your pool is operating <3
----------------------------------------------------------------------------------------------------------------------------------------------------------------------
# Now that you have your pool running, you need to add the coins so that your users can mine
> I will give three examples, installing dogeseedz, and tubopay
#### 1 - Download wallet-qt or COIND of the currency you want to install, remembering some coins are working in yiimp with COIND
![This is an image](https://i.imgur.com/F1pB4El.png)
#### 1.2 - Run wallet-qt or coinD and let it sync
> Depending on your coin, it can take minutes, hours, days, or weeks.
#### 2 - After synchronization, go to your pool, and open the admin portal, after that click on add coin
![This is an image](https://i.imgur.com/QQj6Ey2.png)
#### 2.2 - Fill in the currency information, name, symbol, algorithm, logo, and click save
![This is an image](https://i.imgur.com/f4Amdze.png)
#### 2.3 - Now search for your coin name and click on its symbol
![This is an image](https://i.imgur.com/CmeoU6m.png)
#### 2.4 - Configure what is marked in red, to the settings you want
> - First in general, set the minimum payment
> 
![This is an image](https://i.imgur.com/U9XLxM7.png)
> - In settings, enable the boxes: enable, auto ready, visible, installed, and watch, below them configure the character of the pool (must be generated by wallet-qt or coind ex: ./coind-cli getnewaddress ) in case of dogessed needs enable use segwit too
> 
![This is an image](https://i.imgur.com/tTjPQ85.png)
> - On the exchange tab, do not move unless you have enabled auto exchange in the installation
> -  In the Daemon tab fill in the process name example: dogeseedz-qt or dogeseedzd, after that if your daemon is on the same machine as your pool, put the ip 127.0. of the rpc of the coin (you can put whatever you want), username and password, in rpc type put POW (Attention several coins are POS, seek to inform yourself with the official website of the coin you are installing), after that go to to save

![This is an image](https://i.imgur.com/spgS37c.png)
> - Now find your coin again and click on its symbol, and go straight to the Daemon tab, it will generate a config for your coin, copy only the red part, and put it in your coin config (example: ./dogeseedz/Dogeseedz. conf ) before saving change the path of blocknotify, in my case it is installed in /usr/bin/blocknotify.sh

![This is an image](https://i.imgur.com/ZZwx6gN.png)
> - Your coin config will look like this

![This is an image](https://media.discordapp.net/attachments/932109857698488330/946134365954510848/tuto.png)

#### - Now let's start the stratum for coin
> - Go to your terminal and type: addport fill in the symbol and algorithm of the coin you created, example:( Symbol: SEED Enter, Algo scrypt Enter )

![This is an image](https://media.discordapp.net/attachments/932109857698488330/946137311907831818/addportteste.png)
![This is an image](https://media.discordapp.net/attachments/932109857698488330/946137311530340423/addportalgo.png)
![This is an image](https://media.discordapp.net/attachments/932109857698488330/946137311723274260/addportdone.png)

> - Take the generated port, go back to your coin configuration, in the daemon tab, under POW or POS, you put the stratum port, click on save and your coin is working

![This is an image](https://media.discordapp.net/attachments/932109857698488330/946138001120055366/porta.png?width=840&height=559)

#### In the currency TUBOPAY, LITECOIN, BITCOIN, DASH, DIGIBYTE, and several others, you must turn off the has getinfo box, so that the wallet can communicate with the pool
![This is an image](https://media.discordapp.net/attachments/932109857698488330/946139203425665095/tubohas.png?width=800&height=559)

---------------------------------------------------------------------------------------------------------------------------------------------------------------------
# If this tutorial helped you, make a contribution
# BTC: 1Ljwbwd6Z2UDkscDroHdnave1hzmjApmCD
# LTC: LeVPHyxkvGQ4fFW9DFGPYS6deNWY1AcSBo
# DOGE: DE38DhPsxH8mub5XVhJZxFgKHMbUXhLEMp
# ETH: 0x4da146cfd87bb6ede98bd7ef78791efc281dde3b
