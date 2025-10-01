# SadServers “Kihei” – LVM + Mount Walk-through
https://sadservers.com/scenario/kihei
---

## Scenario

The challenge required creating a data directory with enough space for the app to run. The root filesystem was too small, but additional 1 GB disks were available.  
The solution was to combine these disks with **LVM**, create a logical volume, format it, mount it at `/home/admin/data`, fix permissions, and rerun the app until the checker passed.

---

## TL;DR (Fix Summary)

1. Initialize extra disks as **Physical Volumes**.  
2. Combine them into a **Volume Group**.  
3. Create a **Logical Volume (~1.9G)** spanning both disks.  
4. Format it with `ext4`.  
5. Mount it on `/home/admin/data` and adjust ownership.  
6. Run the app again – it now succeeds.

---

## Step-by-step Command History (trimmed)
```bash
# Inspect app
cd /home/admin
./kihei -v

# Inspect disks
lsblk -l

# 1) Turn the two 1G disks into PVs
sudo pvcreate /dev/nvme1n1
sudo pvcreate /dev/nvme2n1

# 2) Create a VG that spans both PVs
sudo vgcreate new_vol_group /dev/nvme1n1 /dev/nvme2n1
sudo vgs

# 3) Create a ~1.9G LV from the VG
sudo lvcreate -L 1.9G -n new_logical_volume new_vol_group
sudo lvs

# 4) Make filesystem
sudo mkfs.ext4 /dev/new_vol_group/new_logical_volume

# 5) Mount at the app's expected data path
sudo mkdir -p /home/admin/data
sudo mount /dev/new_vol_group/new_logical_volume /home/admin/data
sudo chown admin:admin /home/admin/data

# 6) (Optional) Verify space
df -h /home/admin/data

# 7) Run the challenge binary
./kihei -v

---

## Full Command History (as executed)

```bash
1  history
2  lsblk
3  pvcreate /dev/nvme1n1
4  sudo pvcreate /dev/nvme1n1
5  pvs
6  sudo pvs
7  lsblk
8  lsblk -l
9  sudo pvcreate /dev/nvme0n1
10 sudo pvcreate /dev/nvme2n1
11 sudo pvs
12 gcreate new_vol_group /dev/nvme0n1 /dev/nvme2n1
13 vgcreate new_vol_group /dev/nvme0n1 /dev/nvme2n1
14 sudo vgcreate new_vol_group /dev/nvme0n1 /dev/nvme2n1
15 sudo vgcreate new_vol_group /dev/nvme1n1 /dev/nvme2n1
16 vgs
17 sudo vgs
18 lvcreate -L 1.9G -n new_logical_volume new_vol_group
19 sudo lvcreate -L 1.9G -n new_logical_volume new_vol_group
20 sudo lvs
21 mkfs.gfs2 -p lock_nolock -j 1 /dev/new_vol_group/new_logical_volume
22 gfs2
23 cd /home/admin
24 ls -ltr
25 df -h .
26 df -T -a
27 df -T .
28 mkfs.ext4 -p lock_nolock -j 1 /dev/new_vol_group/new_logical_volume
29 mkfs.ext4 --help
30 sudo mkfs.ext4 /dev/new_vol_group/new_logical_volume
31 df -h .
32 df -h a
33 df -h -a
34 ls -blk
35 lsblk
36 ./kihei -v
37 sudo mount /dev/new_vol_group/new_logical_volume /home/admin/data
38 df -h .
39 df -h /home/admin/data
40 blkid
41 blkid --help
42 blkid -l
43 clear
44 ./kihei
45 ls
46 ls -ltr data
47 ./kihei -v
48 df -h .
49 df -h *
50 cd /home/admin/data/
51 ls -ltr
52 rm -rf lost+found/
53 sudo rm -rf lost+found/
54 cd ..
55 ls -ltr
56 sudo chown admin data
57 ./kihei -v
58 history
