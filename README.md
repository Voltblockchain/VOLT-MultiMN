# Multiple MasterNode

A script which is easily create Multiple Masternodes of the same coin in the same VPS.

First of all you have to start one masternode using <a href="https://github.com/Voltblockchain/VOLT-MN/blob/main/VOLT-MN.sh">VOLT-MN.sh</a> script that is your MainNode.

# Guide of use VOLT-MN.sh for MainNode:

```
wget -q https://raw.githubusercontent.com/Voltblockchain/VOLT-MN/main/VOLT-MN.sh
sudo chmod +x VOLT-MN.sh
./VOLT-MN.sh
```
***

# Guide for Install MultiMN:

Install the multimn script 

`curl -sL https://raw.githubusercontent.com/Voltblockchain/VOLT-MultiMN/main/multimn_install.sh | sudo -E bash -`

Add the coin profile.
```
wget -q https://raw.githubusercontent.com/Voltblockchain/VOLT-MultiMN/main/profiles/volt.mn
multimn profadd volt.mn volt
```
Now the volt profile is saved and the downloaded file can be removed if you want: `rm -rf volt.dmn`

Stop the volt Service:
```
volt-cli stop
systemctl stop volt
```
Now create 3 extra instances with bootstrap (Ex. You want to make 3 Masternode):
```
multimn install volt --bootstrap
multimn install volt --bootstrap
multimn install volt --bootstrap
```
You can check every MN like this:
```
volt-cli-1 getinfo
volt-cli-2 getinfo
volt-cli-3 getinfo
volt-cli-all getinfo
```
There's also a `volt-cli-0`, that is a reference to the 'main node', not a created one with multimn.

Now, if you want to uninstall any instances,then just uninstall it with:

`multimn uninstall volt 2` (Uninstall instance 2)

You can uninstall all of them with:

`multimn uninstall volt all`


You can get priv key of all MN with:

`multimn list volt --privkey`


Note this all priv key and make `masternode.conf` in your Coldwallet where you done MasternodeTx.
so `masternode.conf` look like this:
```
MN0 IP:7160 MN_PrivKey Tx_Hash Output_Index
MN01 IP:7160 MN_PrivKey Tx_Hash Output_Index
MN02 IP:7160 MN_PrivKey Tx_Hash Output_Index
MN03 IP:7160 MN_PrivKey Tx_Hash Output_Index
```

Here IP and port Same for all MN.

MN0 is your main_node MN which you create with <a href="https://github.com/Voltblockchain/VOLT-MN/blob/main/VOLT-MN.sh">VOLT-MN.sh</a> script.

MN01, MN02, MN03 is your masternode which you create with multimn.


Now StartMasternode from Coldwallet with:
```
startmasternode alias false MN0
startmasternode alias false MN01
startmasternode alias false MN02
startmasternode alias false MN03
```

Now StartMasternode in VPS with Service:

`systemctl start volt` (Start your MN which is create with main_node <a href="https://github.com/Voltblockchain/VOLT-MN/blob/main/VOLT-MN.sh">VOLT-MN.sh</a> script)

Below 3 MN which is create with `multimn` script.
```
systemctl start   volt-1.service
systemctl start   volt-2.service
systemctl start   volt-3.service
```

That's all now your MN start.