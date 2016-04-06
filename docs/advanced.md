# Advanced Configurations

The [`ovpn_genconfig`](/bin/ovpn_genconfig) script is intended for simple configurations that apply to the majority of the users.  If your use case isn't general, it likely won't be supported.  This document aims to explain how to work around that.

## Create host volume mounts rather than data volumes

* Refer to the Quick Start document, and substitute `--volumes-from $OVPN_DATA` with `-v /path/on/host/openvpn0:/etc/openvpn`
* Quick example that is likely to be out of date, but here's how to get started:

        mkdir openvpn0
        cd openvpn0
        docker run --rm -v $PWD:/etc/openvpn beznosa/openvpn-mikrotik ovpn_genconfig -u tcp://VPN.SERVERNAME.COM:443
        docker run --rm -v $PWD:/etc/openvpn -it beznosa/openvpn-mikrotik ovpn_initpki
        vim openvpn.conf
        docker run --rm -v $PWD:/etc/openvpn -it beznosa/openvpn-mikrotik easyrsa build-client-full CLIENTNAME nopass
        docker run --rm -v $PWD:/etc/openvpn beznosa/openvpn-mikrotik ovpn_getclient CLIENTNAME > CLIENTNAME.ovpn

* Start the server with:

        docker run -v $PWD:/etc/openvpn -d -p 443:1194/tcp --privileged beznosa/openvpn-mikrotik
