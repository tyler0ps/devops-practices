# SadServers — Scenario: "Bondo": Split my pile!

[https://sadservers.com/newserver/bondo](https://sadservers.com/newserver/bondo)

---

## Scenario

---

In this challenge, the `/srv/bondo` directory was running out of space, causing the `/home/admin/bondo` binary to fail when generating output files.
The task required **identifying the storage issue** and **expanding the logical volume** used by `/srv/bondo` so that the tool could successfully complete its operation.

---

## TL;DR (Fix Summary)

---

* Verified that the `/srv/bondo` partition was full.
* Identified that it resided on a logical volume `/dev/vg-backup/lv-bondo`.
* Extended the underlying physical volume `/dev/nvme1n1`.
* Extended the logical volume to use all remaining free space.
* Resized the filesystem with `resize2fs`.
* Re-ran `/home/admin/bondo` successfully and confirmed with the check script.

---

## Step-by-step Command History (trimmed)

---

1. Checked directory and disk usage:

   ```bash
   ls /srv/bondo
   df -h /srv/bondo
   du -h /srv/bondo
   ```

   → Found that `/srv/bondo` volume was nearly full.
2. Inspected block devices and LVM structure:

   ```bash
   lsblk
   sudo vgs
   sudo lvs
   sudo pvs
   ```
3. Verified existing volume group and logical volume:

   ```bash
   sudo vgdisplay vg-backup
   sudo lvdisplay /dev/vg-backup/lv-bondo
   ```
4. Extended the physical volume (to claim new space):

   ```bash
   sudo pvresize /dev/nvme1n1
   ```
5. Extended the logical volume to use all free space:

   ```bash
   sudo lvextend -l +100%FREE /dev/vg-backup/lv-bondo
   ```
6. Resized the filesystem to fill the expanded LV:

   ```bash
   sudo resize2fs /dev/vg-backup/lv-bondo
   ```
7. Verified space after expansion:

   ```bash
   df -h /srv/bondo
   ```
8. Ran the application again:

   ```bash
   /home/admin/bondo
   ```
9. Confirmed with the check script:

   ```bash
   /home/admin/agent/check.sh
   ```

---

## Full Command History (as executed)

---

```
 1  /home/admin/bondo
 2  ls
 3  cd /srv/bondo/
 4  ls
 5  cd ..
 6  ls -ltr
 7  df -h
 8  df -h .
 9  /home/admin/bondo -v
10  /home/admin/bondo gen
11  /home/admin/bondo check
12  df -h /srv/bondo/
13  cat /srv/bondo/part-7de9eb669d8303f0b145815f69e3360.bin:
14  ls -ltr /srv/bondo/part-7de9eb669d8303f0b145815f69e3360.bin:
15  cd /srv/bondo/
16  ls
17  rm *
18  ls
19  cd lost+found/
20  ls -ltr
21  df -h 
22  df -h  .
23  du -h .
24  sudo du -h lost+found/
25  history
26  /home/admin/bondo
27  df -h /home/admin/
28  cd /
29  df -h
30  lsblk
31  - L
32  - l
33  lsblk -l
34  vgl
35  vg list
36  which vg
37  which vgs
38  vgs
39  which lvcreate
40  sudo vgs
41  sudo lvs
42  sudo pvs
43  sudo pvcreate /dev/nvme1n1
44  du /srv/bondo
45  sudo du -h/srv/bondo
46  sudo du -h /srv/bondo
47  sudo vgdisplay vg--backup
48  sudo vgdisplay /dev/sdb
49  sudo vgdisplay vg-backup
50  sudo pvdisplay /dev/nvme1n1
51  sudo pvresize /dev/nvme1n1
52  sudo lvextend -L 1G /dev/vg-backup/lv--bondo
53  sudo vgdisplay vg-backup 
54  sudo lv display
55  sudo lvdisplay
56  sudo lvdisplay /dev/vg-backup/lv-bondo
57  df -T /srv/bondo 
58  sudo lvextend -l +100%FREE /dev/vg-backup/lv-bondo
59  sudo resize2fs /dev/vg-backup/lv-bondo 
60  sudo vgdisplay vg--backup | grep -E "Free|Size"
61  sudo vgdisplay vg-backup | grep -E "Free|Size"
62  sudo file -sL /dev/vg-backup/lv-bondo
63  ls
64  sudo df -h /srv/bondo
65  history
66  /home/admin/bondo
67  /home/admin/agent/check.sh
68  history
```