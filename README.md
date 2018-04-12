## Funding your Masternode

* First, we will do the initial collateral TX and send exactly 5000 BWK to one of our addresses. To keep things sorted in case we setup more masternodes we will label the addresses we use.

  - Open your BWK wallet and switch to the "Receive" tab.

  - Click into the label field and create a label, I will use MN1

  - Now click on "Request payment"

  - The generated address will now be labelled as MN1 If you want to setup more masternodes just repeat the steps so you end up with several addresses for the total number of nodes you wish to setup. Example: For 10 nodes you will need 10 addresses, label them all.

  - Once all addresses are created send 5000 BWK each to them. Ensure that you send exactly 5000 BWK and do it in a single transaction. You can double check where the coins are coming from by checking it via coin control usually, that's not an issue.

* As soon as all 5k transactions are done, we will wait for 15 confirmations. You can check this in your wallet or use the explorer. It should take around 30 minutes if all transaction have 15 confirmations

## Installation & Setting up your Server

Generate your Masternode Private Key

In your wallet, open Tools -> Debug console and run the following command to get your masternode key:

```bash
masternode genkey
```

Run this command to get your output information:

```bash
masternode outputs
```

Copy both the key and output information to a text file.

Close your wallet and open the Bulwark Appdata folder. Its location depends on your OS.

* **Windows:** Press Windows+R and write %appdata% - there, open the folder Bulwark.  
* **macOS:** Press Command+Space to open Spotlight, write ~/Library/Application Support/Bulwark and press Enter.  
* **Linux:** Open ~/.bulwark/

In your appdata folder, open masternode.conf with a text editor and add a new line in this format to the bottom of the file:

```bash
masternodename ipaddress:52543 genkey collateralTxID outputID
```

An example would be

```
mn1 127.0.0.2:52543 93HaYBVUCYjEMeeH1Y4sBGLALQZE1Yc1K64xiqgX37tGBDQL8Xg 2bcd3c84c84f87eaa86e4e56834c92927a07f9e18718810b92e0d0324456a67c 0
```

_masternodename_ is a name you choose, _ipaddress_ is the public IP of your VPS, masternodeprivatekey is the output from `masternode genkey`, and _collateralTxID_ & _outputID_ come from `masternode outputs`. Please note that _masternodename_ must not contain any spaces, and should not contain any special characters.

Restart and unlock your wallet.

SSH (Putty on Windows, Terminal.app on macOS) to your VPS, login as root, and install git if it isn't installed already.

```bash
apt-get -y install git
```

Then clone the Github repository.

```bash
git clone https://github.com/bulwark-crypto/Bulwark-MN-Install
```
Navigate to the install folder:

```bash
cd Bulwark-MN-Install
```

Install & configure your desired master node with options.

```bash
bash install.sh
```

When the script asks, input your VPS IP Address and Private Key (You can copy your private key and paste into the VPS if connected with Putty by right clicking)

Follow the instructions on screen.

After the basic installation is done, the wallet will sync. You will see the following message:

```
Your masternode is syncing. Please wait for this process to finish.
This can take up to a few hours. Do not close this window.
```

It's possible you'll see errors like  `error: {"code":-28,"message":"Loading wallet... (73.73 %)"}` - this is fine, just wait for the wallet to finish syncing, afterwards your masternode will start.

Once you see "Masternode setup completed." on screen, you are done.

## Refreshing Node

If your masternode is stuck on a block or behaving badly, you can refresh it.
Please note that this script must be run as root.

```
rm -rf Bulwark-MN-Install && git clone https://github.com/bulwark-crypto/Bulwark-MN-Install && cd Bulwark-MN-Install && bash refresh_node.sh
```

No other attention is required.

## Updating Node

To update your node please run this command and follow the instructions.
Please note that this script must be run as root.

```
rm -rf Bulwark-MN-Install && git clone https://github.com/bulwark-crypto/Bulwark-MN-Install && cd Bulwark-MN-Install && bash update_node.sh
```
