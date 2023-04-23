## INSTRUCTIONS

**1. Define volume name variable**

OVPN_DATA="docker-openvpn_ovpn-data"

**2. Create the volume**

docker volume create --name $OVPN_DATA

**3. Generate configuration**

(It will ask for a phase to define keys. You can use any type of word)

docker-compose run -v $OVPN_DATA:/etc/openvpn --rm vpn ovpn_genconfig -u udp://vpn.dummydomain.click

docker-compose run -v $OVPN_DATA:/etc/openvpn --rm  vpn ovpn_initpki

- This is goign to ask for phrase key. Put whatever phrase you want.
- Then is going to ask for the host name, Type in the domain you have setup for this server (vpn.dummydomain.click)

**4. Generate client files**

docker-compose run -v $OVPN_DATA:/etc/openvpn --rm vpn easyrsa build-client-full CLIENTNAME nopass

docker-compose run -v $OVPN_DATA:/etc/openvpn --rm vpn ovpn_getclient CLIENTNAME > CLIENTNAME.ovpn

This last command is going to generate the client configuration file that will allow you 
to connect from your PC or mobile device.
