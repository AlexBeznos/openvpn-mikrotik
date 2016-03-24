# Static IP Addresses

The docker image is setup for static client configuration on the 192.168.254.0/24 subnet.  To use it follow the Quick Start section below.  Note that the IP addresses octets need to be picked special, see [OpenVPN Documentation](https://openvpn.net/index.php/open-source/documentation/howto.html#policy) for more details.

## Quick Start

1. Create a client specific configuration:

        $ docker run --volumes-from $OVPN_DATA --rm -it beznosa/docker-openvpn-staticip ovpn_staticip CLIENTNAME CLIENTIP SERVERIP
        ifconfig-push 192.168.254.1 192.168.254.2

2. Wait for client to reconnect if necessary

## Advanced Admin

Login to the data volume with a `bash` container, note only changes in /etc/openvpn will persist:

    docker run --volumes-from $OVPN_DATA -it --rm beznosa/docker-openvpn-staticip bash -l

## Upgrading from Old OpenVPN Configurations

If you're running an old configuration and need to upgrade it to pull in the ccd directory run the following:

    docker run  --volumes-from $OVPN_DATA --rm beznosa/docker-openvpn-staticip ovpn_genconfig
