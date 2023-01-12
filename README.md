
OVPN_DATA="docker-openvpn_ovpn-data"

1) docker-compose run -v $OVPN_DATA:/etc/openvpn --rm vpn ovpn_genconfig -u udp://vpn.dummydomain.click
2) docker-compose run -v $OVPN_DATA:/etc/openvpn --rm -it vpn ovpn_initpki

docker-compose run -v $OVPN_DATA:/etc/openvpn --rm -it vpn easyrsa build-client-full CLIENTNAME nopass
docker-compose run -v $OVPN_DATA:/etc/openvpn --rm vpn ovpn_getclient CLIENTNAME > CLIENTNAME.ovpn



docker run -d -p 1194:1194/udp --cap-add=NET_ADMIN test/openvpn