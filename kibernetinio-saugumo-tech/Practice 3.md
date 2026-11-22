## Ex1
**Exercise**: proxy from home PC to uosis server to VM
VM:
```
sudo apt install python3
echo "welcome to : $(hostname -I)" > index.html
python3 -m http.server 8080 --bind 127.0.0.1 &
curl 127.0.0.1:8080
```

Home PC:
`ssh -i ~/.ssh/id_ed25519 -J augr3377@uosis.mif.vu.lt -L 8080:127.0.0.1:8080 augr3377@193.219.91.103 -p 5698`

## Ex2
**Exercise**: proxy 3 machines M1 -> M2 (lab2_2 as a `proxychains4`) -> M3

proxychains4 curl http://10.0.1.197/flag.txt

To run a server:
microsocks -i 0.0.0.0 -p 1080

