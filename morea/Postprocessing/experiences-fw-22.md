---
title: " Setup Metashape on a cluster "
published: true
morea_id: experience-fw-22
morea_summary: "Setup Metashape on a cluster"
morea_url: 
morea_type: experience
morea_sort_order: 22
morea_labels:
 - preliminary 
 - knowledgebase
---

# Setup Metashape on a cluster 
The concept is roughly outlined in chapter 8 of the [Photoscan Manual](https://www.agisoft.com/pdf/metashape-pro_1_8_en.pdf). Nevertheless there are some pitfalls and not so well documented features.

First you need to export a common net ressource. You may follow the [digitialocean](https://www.digitalocean.com/community/tutorials/how-to-set-up-an-nfs-mount-on-ubuntu-16-04)example:

```bash
# on the sever side (exporting machine)
sudo apt-get install nfs-kernel-server
sudo mkdir /var/nfs/general -p
sudo chown nobody:nogroup /var/nfs/general
sudo nano /etc/exports
/var/nfs/general    xxx.xxx.xxx.xxx(rw,sync,no_subtree_check)
sudo systemctl restart nfs-kernel-server

# on the clients side
sudo apt-get install nfs-common
sudo mkdir /var/nfs/agi -p
sudo mount xxx.xxx.xxx.xxx:/var/nfs/general /var/nfs/agi

```

Now you have to start a head node as photoscan server

```bash
nohup ./photoscan.sh --server xxx.xxx.xxx.xxx --dispatch xxx.xxx.xxx.xxx  --root /var/nfs/agi
```

Next you may assign node(s)

```bash

nohup ./photoscan.sh --node --dispatch xxx.xxx.xxx.xxx  --opencl_gpu_mask 1  --root /var/nfs/agi
```


{% include note.html content=" 
 
Be aware, that the monitor and the network installation of Agisoft Photoscan **must** have the same version.
The installation on the computer may have a newer version.
 

"
%}
