## INSTRUCTIONS

**1. Define volume name variable**

OVPN_DATA="docker-openvpn_ovpn-data"

**2. Create the volume**

docker volume create --name $OVPN_DATA

**3. Generate configuration**

(It will ask for a phase to define keys. You can use any type of word)
docker-compose run -v $OVPN_DATA:/etc/openvpn --rm vpn ovpn_genconfig -u udp://vpn.dummydomain.click
docker-compose run -v $OVPN_DATA:/etc/openvpn --rm  vpn ovpn_initpki

**4. Generate client files**
docker-compose run -v $OVPN_DATA:/etc/openvpn --rm vpn easyrsa build-client-full CLIENTNAME nopass
docker-compose run -v $OVPN_DATA:/etc/openvpn --rm vpn ovpn_getclient CLIENTNAME > CLIENTNAME.ovpn