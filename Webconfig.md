# 1. Web settings
Install apache 2
```bash
	sudo apt update
	sudo apt install apache2 -y
```
download and install cgi file
```bash
	sudo cp qcmap_web_cgi.cgi /usr/lib/cgi-bin
	sudo cp qcmap_auth.cgi /usr/lib/cgi-bin
	sudo chmod 777 * /usr/lib/cgi-bin
 ```
Enable cgi mode
```bash
	cd /etc/apache2/mods-enabled
	sudo ln -s ../mods-available/cgi.load
	cd /var/www/html/
	sudo ln -s  /usr/lib/cgi-bin
 ```
 Update html file 
 
 ```bash
	sudo cp -R  * /var/www/html/
	sudo chown -R www-data:www-data /var/www/html/
 ```
 Restart apache service
 
 ```bash
	sudo /etc/init.d/apache2  restart
 ```
# 2. Load bitstream into FPGA

step 1: Open vivado lab

step 2: Click "Open Hardware Manager"

step 3: Right click "auto connection"

step 4: Right click "local host" => "Add Xilinx Virtual Cable (XVC)"

step 5: update E300 Box's IP address and port  (FPGA1 : port 2541 ; FPGA2: port 2542; FPGA3: port 2543)

step 6: Right click "vu35p/xcu50..." => "Program device" => linking to bitstream file => "program"


# 3. Running miner
There are two options for run miner

Option 1: Run miner by command line
```bash
	sudo  ./ethminer --fpga -a 530 -b 312 -c 125 -q 100 -e 4 -f -d 60  -P stratum1+tcp://0x2784685ba4a940406b185f945c26104d64f7562e.vu35p@eth-na.f2pool.com:6688 
```
_Note_ 
 
 ` -e 1 : Mode auto-tunning mode (Miner will find the best frequency and run it)`

 ` -e 4 : Mode manual  (Miner will receive input clock parameters from command line `


Option 2: Run miner by script
```bash
	sudo  ./startMiner.sh
```

