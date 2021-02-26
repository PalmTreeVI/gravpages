---
title: 'Masternode Setup Guide'
date: '24-02-2021 19:24'
taxonomy:
    category:
        - Masternodes
    tag:
        - masternode
        - vps
    author:
        - 'Alice Adams'
---

#### Introduction

This tutorial will guide you in detail through the steps necessary to setup a PIVX masternode on Ubuntu 18.04 64-bit remote server (VPS) that is controlled via your local Control wallet. Your local wallet is not required to be kept open and you can store it as a cold wallet whilst still collecting masternode payments. There are other ways to setup masternode, but this one is highly recommended as it’s one of the most secure ways. If you need any additional help, feel free to join PIVX Discord and ask for a help in #support channel. DO NOT receive any help or assistance through private messages, because there are many impersonators showing up as PIVX team members that are trying to steal coins from you! They might look legit, but it’s high likely they are scammers. No one ever from PIVX team will contact you privately and offer you help. Every help will be offered in public support channel!


#### Basic requirements:


* Local system – your everyday computer, which will run Control wallet and hold the masternode coins
* Remote VPS with Ubuntu Server 18.04 64-bit OS installed with unique IP address that is running 24/7
* Minimum VPS specs: 50 GB of storage space, 2 GB of RAM, 1 dedicated CPU core
* Latest PIVX Core wallet release: v5.0.1
* 10,000 PIVX (good to have 10,001 to make sure you can cover transaction fee)

!! (NOTE: You will need a different IP address for each masternode you plan to host.)  

#### Configuration of your Control wallet

**Step 1** – Download PIVX wallet


Download the most recent version of the PIVX Core wallet here:

https://github.com/PIVX-Project/PIVX/releases/latest


**Step 2** – Extract and install the wallet


Choose the proper version for your operating system. Extract it, install and run the wallet. After starting the wallet for the first time, it will offer you to make a default PIVX data directory. Depending on your operating system, the default directory should be similar to:

C:\Users\YourUsername\AppData\Roaming\PIVX


The above example of default directory is Windows based.

If you choose your own location ensure that you record where that is.


**Step 3** – Create a Masternode using Creation Wizard


First of all, make sure that you have 10,000 PIV in your wallet (in fact, 10,001 PIV to make sure you are able to cover the transaction fees).


    Unlock the wallet.
    Go to “Masternodes” tab.
    Click “Create Masternode Controller“.
    masternode-Tutorial1
    Masternode Creation Wizard intro window will open. It just reminds you that you need to have 10,000 PIV in your wallet in order to create a Masternode. Just click the “Next” button.
    masternode-Tutorial2
    Now you need to type the Masternode name as per your wish (i.e. “Masternode01”) and then click “Next” button again.
    masternode-Tutorial3
    Now you will be asked to type the IP address of your VPS (it might look similar to “182.214.90.12”), and then click “Next” button again.
    masternode-Tutorial4
    If everything went successful, you should get a message “Master node created!”.
    masternode-Tutorial5
    Status of the newly created Masternode will be “MISSING”. That is normal in this phase.
    masternode-Tut2

We will get back here to Control wallet little bit later after we setup VPS.


#### VPS Remote wallet installation

These procedures are for a clean server install. If you have an existing installation then some steps may not be required. Performing the steps is unlikely to have any effect on the system. Securing the server has NOT been included in this tutorial. That is your responsibility. Although it’s not required, a great guide can be found here to assist you.


To be able to access a VPS, you need a software/SSH client like PuTTY for example. You can choose between alternatives as well, but this tutorial will not include installation of such software. After you successfully login to your VPS, follow the further steps.


**Step 1** – Install most recent security patches


A clean server install will likely need some software updates. Enter the following command which will bring the system up to date:


    sudo apt-get update && sudo apt-get -y upgrade

Step 2 – Download and extract PIVX Core wallet for Linux


Enter the following command lines one by one to download and extract PIVX wallet:


    cd ~ && wget https://github.com/PIVX-Project/PIVX/releases/download/v5.0.1/pivx-5.0.1-x86_64-linux-gnu.tar.gz

    tar -zxvf pivx-5.0.1-x86_64-linux-gnu.tar.gz && sudo rm -f pivx-5.0.1-x86_64-linux-gnu.tar.gz


Masternode Configuration

Step 3 – Create the masternode configuration file and populate


Before the node can operate as a masternode a custom configuration file needs to be created. Since we have not loaded the wallet yet, we will create the necessary directories and the configuration file by typing the following command lines one by one:


    mkdir ~/.pivx && cd ~/.pivx && sudo apt-get install nano && touch pivx.conf && nano pivx.conf

This command has created a blank PIVX configuration file where we will enter our masternode configuration variables. Now we should properly setup configuration settings.


Paste the following configuration settings into the editor (using PuTTY, paste is being done simply by right mouse click):


    rpcuser=<YOUR_OWN_RPC_USERNAME>

    rpcpassword=<YOUR_OWN_RPC_PASSWORD>

    rpcallowip=127.0.0.1

    server=1

    daemon=1

    maxconnections=256

Before you exit the editor, there are 3 parameters that you need to update with your own settings. These are:


    <YOUR_OWN_RPC_USERNAME> – Set this to a custom username. i.e. rpcuser
    <YOU_OWN_RPC_PASSWORD> – Set this to a STRONG password. i.e. password<– NO!!! Use something more complex for your own safety!
    Now go back to Control wallet in Masternode tab, click on the 3 dots next to Masternode you created few steps above and then click “Info“.
    masternode-Tutorial6
    Now click icon next to “Export data to run the Masternode on a remote server“.
    masternode-Tut1
    It will now ask you for a confirmation to export required data to run a Masternode. Click “OK” button.
    masternode-Tutorial7
    Now you will get a message that required info was successfully exported (copied to your clipboard) and now you should paste it in your pivx.conf file on your VPS under themaxconnections=256 line in pivx.conf file.
    masternode-Tutorial8
    After all, your pivx.conf file on your VPS should look like:

        rpcuser=root
        rpcpassword=PasswordOfYourChoice
        rpcallowip=127.0.0.1
        server=1
        daemon=1
        maxconnections=256
        masternode=1
        externalip=101.168.87.207
        masternodeaddr=101.168.87.207:51472
        masternodeprivkey=87haGjw6ABVZfZTcMNX5c1E3HUVH4qWcdc823RBDHsGC5P8FohW

    Save and exit the editor by pressingCTRL-Oand Enterto save andCTRL-Xto exit the editor.


    Start your masternode
    Step 4 – Load the masternode
    With the configuration created we are now ready to load the masternode and sync to the network. Load the masternode by typing the following command:

        cd ~/pivx-5.0.1/bin && ./pivxd

    You will get the message “PIVX server starting”. To follow the progress until the wallet is fully loaded and synchronized, type:

        tail -f ~/.pivx/debug.log

    Wait until you see the message similar to:
    2020-01-10 13:31:01 CMasternodeSync::GetNextAsset – Sync has finished
     2020-01-10 13:31:01 CActiveMasternode::ManageStatus() – not capable: Hot node, waiting for remote activation.
    Once you get this message, you are completely synced and masternode is ready to be started. PressCTRL-C to get back to command line.
    ________________________________________________________________________________________________________________
     *EXTRA STEP ONLY IF YOU DON’T SEE THESE 2 LINES/MESSAGES ANYWHERE:

        ./pivx-cli getbestblockhash

    You will get back hash that will look like:
    1ab2a12a1a1a121a1212ab1aba121212121ab1a1a12a12121aba1a1abab1212aa1
    Paste the number you get after./pivx-cli reconsiderblockcommand like this:

        ./pivx-cli reconsiderblock 1ab2a12a1a1a121a1212ab1aba121212121ab1a1a12a12121aba1a1abab1212aa1

    Finally, type:

        ./pivx-cli clearbanned

    ________________________________________________________________________________________________________________
    NOTE: Wait for 15 confirmations on the blockchain for transaction with the masternode collateral before proceeding with the next steps below.
    Now go back to your Control wallet -> Masternodes -> Click “Start Inactive/s”
    Status will change from MISSING -> ACTIVE.
    masternode-Tutorial9
    Now go back to your VPS and type:
    ./pivx-cli startmasternode local false

    If everything went well, you should receive the following message:
    “Masternode successfully started”
    Congratulations! You have successfully started your masternode!
    ADDITIONAL NOTES:
    1) if the output of getmasternodestatus is fine, then you are perfectly fine. But have in mind that it can take up to 2 hours for masternode to change status from ACTIVE to ENABLED in the masternode list.
    2) First masternode reward requires a longer waiting period. It usually takes 3-5 days to receive a first masternode reward.
    3) You can close the Control wallet, as it is not needed. Only VPS should be working 24/7.
    If you have any troubles or issues, feel free to join PIVX Discord and post your question in #support channel. Again, DO NOT ever receive any help or assistance through private messages, as there are many scammers out there trying to steal your coins, even if they look the same as developers, admins or support staff. Every help ever will be provided through public channels.
    Shutting down a Masternode

        1) How do I stop running masternode on my VPS and delete masternode from my PIVX Control wallet?

    a) In Control wallet in Masternode tab click on Masternode you wish to shutdown and click “Delete”.
    b) Restart the wallet.
    c) Your 10,000 coins are now unlocked and spendable.

        2) How do I get the 10,000 PIVX back that I’ve send to my Masternode address at the beginning?

    You don’t need to “get it back” as it is already in your wallet.
    Being in the different address is not an issue as that’s also your address.

        3) Can I use this 10,000 PIVX normally on my wallet then again, and sell it or stake it normally like before?

    Yes! If your wallet is unlocked for staking, it will automatically stake these 10,000 coins and you can spend them at any time.
