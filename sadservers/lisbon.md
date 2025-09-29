https://sadservers.com/scenario/lisbon
"Lisbon": etcd SSL cert troubles

systemctl cat etcd -> --cert-file=/etc/ssl/certs/localhost.crt

sudo openssl req -x509 -new -nodes -key /etc/ssl/certs/localhost.key \
  -sha256 -days 365 -out /etc/ssl/certs/localhost.crt

openssl x509 --noout -dates -subject -issuer -in /etc/ssl/certs/localhost.crt

sudo systemctl restart etcd.service

curl https://localhost:2379/v2/keys/foo

openssl s_client -connect 127.0.0.1:2379 -showcerts </dev/null 2>/dev/null | openssl x509 -noout -dates -subject -issuer

echo | openssl s_client -showcerts -servername localhost -connect localhost:2379 2>/dev/null | openssl x509 -inform pem -noout -text

sudo iptables -t nat -L
sudo iptables -t nat -F

sudo cp /etc/ssl/certs/localhost.crt /usr/local/share/ca-certificates/localhost.crt
sudo update-ca-certificates --fresh
