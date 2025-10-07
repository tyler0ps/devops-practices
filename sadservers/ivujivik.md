https://sadservers.com/newserver/ivujivik

ivujivik

```bash
awk -F, 'BEGIN{max=0;}{if ($9 > max && $4 <100000){max=$9;ans=$2}} END{print ans}' /home/admin/table_tableau11.csv
```