https://sadservers.com/newserver/unimak

unimak

```bash
cat station_information.json | jq '.data[][] | select (.capacity > 30 and .has_kiosk == false) | .station_id' > ~/mysolution
sed -i 's/"//g' /home/admin/mysolution
```
