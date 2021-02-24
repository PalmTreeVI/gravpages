---
title: 'Resync the Blockchain'
date: '14-02-2021 11:40'
taxonomy:
    category:
        - 'Core Wallet'
    tag:
        - wallet
        - syncing
    author:
        - 'Bob Burns'
---

If your PIVX Core blockchain cache has become corrupt or forked, you may wish to resync it using one of the methods below.  **Please note that during the sync your balance will show as 0 until near the end, this is normal and nothing is lost**

**Preparation** - Before trying any of the methods below, please consider these steps

    It is always a good idea to make new wallet.dat and zPIV seed backups
    Make sure you are running the latest version of PIVX Core.  Running old software can be a reason that your wallet forked in the first place and it will likely fork again if you have not updated

#### Method 1 - Resync the blockchain from scratch

(Takes the longest, but it is the easiest.  This method will sync you from block 1 and your computer will download and validate every block.  CPU and bandwidth heavy)

**Graphic User Interface (GUI) users:**

"Tools > Wallet Repair > Delete Local Blockchain Folders (-resync)" to initiate the full re-sync.

**Command line users:**

You can initiate the full resync during daemon startup with the command switch `pivxd -resync`


#### Method 2 - Use a bootstrap

(Medium Difficulty: Takes a medium amount of time to resync.  This will provide a zip that your computer can import and validate blocks from that will save on bandwidth.  CPU heavy)

https://pivx.freshdesk.com/support/solutions/articles/30000021125-using-the-bootstrap


#### Method 3 - Restore a snapshot

(Medium Difficulty: Takes almost no time to sync because it is not downloading or validating any blocks.  Instead you are trusting the data in the snapshot is correct)

https://pivx.freshdesk.com/support/solutions/articles/30000026470-how-can-i-use-a-snapshot-


#### Method 4 - Manual Resync

(Medium Difficulty: Only use this option if all others have failed.  Your computer will download and validate all new blocks.  CPU and bandwidth heavy)

    Gracefully shut down your PIVX wallet
    Navigate to your PIVX data directory and delete ONLY the files noted in the follow image:
    (Do NOT delete backups, masternode.conf, pivx.conf, or wallet.dat)