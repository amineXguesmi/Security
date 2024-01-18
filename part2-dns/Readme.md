## Section 5 : (DNS)

### install dependencies :

run `sudo apt update` `sudo apt install bind9`

### add the ip of the dns server to resolv.conf

run `sudo nano /etc/resolv.conf`

![Untitled](Security%20GL4%202b4a1420bcc445e480f013d3f3de320b/Untitled%2063.png)

### create a forward zone

run `sudo nano /etc/bind/named.conf.local`

![Untitled](Security%20GL4%202b4a1420bcc445e480f013d3f3de320b/Untitled%2064.png)

### create file to contain the hosts :

run

 `sudo mkdir /etc/bind/zones`

 `sudo nano /etc/bind/zones/db.insat.tn`

![Untitled](Security%20GL4%202b4a1420bcc445e480f013d3f3de320b/Untitled%2065.png)

### restart bind service :

run

 `sudo systemctl restart bind9` or

 `sudo systemctl restart named`

### Start the DNS server:

run `/usr/sbin/named -g -c /etc/bind/named.conf -u bind`

![Untitled](Security%20GL4%202b4a1420bcc445e480f013d3f3de320b/Untitled%2066.png)

### Test the DNS server

use the command `nslookup` to test the dns server

![Untitled](Security%20GL4%202b4a1420bcc445e480f013d3f3de320b/Untitled%2067.png)
