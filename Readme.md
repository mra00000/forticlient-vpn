
# Forticlient VPN Docker Image

  

This is a fork of jakubv's foriclient docker image. Support for Microsoft account 2-step authentication has been added, allowing LDAP account to login into Fortigate VPN Client

  

Here's what it do:

>  * Connect and authenticate user into Forigate VPN Server with supplied information and credentials

>  * Map a PC's ip address in the VPN network to user's local network, so that user can perform RDP into targeted PC from any device in user's LAN

  

## Usage

Run the following command to setup the VPN Client

```bash
docker run \
	--name ftcvpn \
	-it \
	--privileged \
	-p 51234:3380 \
	-e "VPNADDR=<server_address>:<port>" \
	-e "VPNUSER=<username>" \
	-e "VPNPASS=<password>" \
	-e "VPNRDPIP=<remote_pc_ip_address>" \
dockerforticlient
```
*Parameters*
* `VPNADDR`: Address and port of the VPN server you wish to connect to, should be in format of `serverAddress:port`
* `VPNUSER`: Username that you want to use to authenticate into VPN Server
* `VPNPASS`: Password of the account
* `VPNRDPIP`: Remote PC's IP address you wish to RDP

After finished setting things up, the container will start connecting you to the VPN Server, if the provided credentials are correct, it will ask you for the Microsoft Verification Code, grab and input the code, then press **++  (plus for 2 times)** to send the code to the container and continue connecting. Once the connecting process is done, you can connect to your targeted PC with the address `127.0.0.1:51234` *(This port can be changed by modifying it in the `docker run` command)*
After done working, you can terminate the VPN Client by pressing `Ctrl+C`. To restart the VPN Client, use this command 
> `docker start -i ftcvpn `

*Note that the docker container's name can also be changed by modifying the `docker run` command*