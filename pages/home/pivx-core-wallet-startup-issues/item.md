---
title: 'PIVX Core Wallet Startup Issues'
date: '14-02-2021 11:41'
taxonomy:
    category:
        - 'Core Wallet'
    tag:
        - wallet
        - error
    author:
        - 'Darren Day'
---

#### **Symptoms**
Your PIVX wallet software does not start.  When you try to run it nothing happens, an error is displayed, the window disappears, the loading window never completes, or another startup issue is encountered

#### **Cause**

An abnormal exit of the wallet could result in corruption of your local blockchain cache. This can happen due to a power loss, unexpected reboot, OS updates, or if the local blockchain cache becomes corrupt by other means.

#### **Resolution**

**Method 1**

  Make a backup of your wallet.dat file and zPIV seed (Best practices)  
  Make sure you are running the latest PIVX Core software  
  Try using the -forcestart startup flag to see if it will recover from a failed start.  
  In the Windows GUI, you will need to make a shortcut to the pivx-qt.exe file  
  Then, edit the shortcut properties and append it to the end of the "Target" field, so that the end reads:pivx-qt.exe" -forcestart
  From the command line on all operating systems you can call the pivxd daemon with the switch -forcestart

**Method 2**

If Method 1 does not resolve the startup issue, try to resync the blockchain using the steps in this link