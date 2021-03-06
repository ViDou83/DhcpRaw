# DCHPRaw
DCHP Raw socket C++ (broadcast mode, relay mode and adding customer DHCP options)

This progam allows to simulate the behavior of a DHCP Client and DHCP relays. 
This program can be only be executed on Windows Server SKU as RAW socket support is needed.

# DhcpRaw Usage :

Version: 1.0

Usage:  
        
        regular mode:   DhcpRaw -i {ifIndex} -n {NbrLeasesWanted} -a

        relay mode  :   DhcpRaw -i {ifIndex} -n {NbrLeasesWanted} -r {RelayAddr} -s {DHCPSrvAddr} -a

`
DchpRaw.exe -h
Usage:  
        
        regular mode:   DhcpRaw -i {ifIndex} -n {NbrLeasesWanted} -a

        relay mode  :   DhcpRaw -i {ifIndex} -n {NbrLeasesWanted} -r {RelayAddr} -s {DHCPSrvAddr} -a

        -i: Specify the ifIndex of the NIC where you want to send out DHCP msg (please run DHCPRaw.exe -d

        -n: Number of DHCP leases you want to request (One DHCPClient by lease => many threads)

        -r: RELAY MODE ONLY: Address ip to borrow as DHCP relay. Alternate IP Addresses will be plumbed on the NIC specified by -i
                Multiple addresse can be added separated by comma

        -s: RELAY MODE ONLY: Specify the ip address of the DHCP server to which the DHCPrelay will send the DHCP messages. To allow the DHCP SRV to respond, please add a default route to this machine or a arp static entry from the DHCP server or a route pointed to the machine where this program is executed

        -d: Dump all local system's adapters settings and attributes

        -a: Automatically send DHCP release for granted lease(s)
            If not specified the DHCP client will enter in all DHCP Client state from INIT to REBINDING. Renew at T1, Rebinding at T2, etc

        -opt: Specify custom opt in Hex format seperate by ,;:/
                Ex for OPT 82 with SubnetSelection 192.168.100.0/24:
                        -opt 0x52,0x6,0x5,0x4,0xc0,0xa8,0x64,0x0

        -paramreqlist: Specify paramaters request list (DHCP opt 55) in Hex format separate by ,;:/.
                Ex SubnetMask,DomainName,Router,NetBIOSopts,DomainNameServer::
                        -paramreqlist 0x1,0xf,0x3,0x2c,0x2e,0x2f,0x6
`
Ex: 

`
PS C:\Users\Administrator\Downloads> .\DHCPRaw.exe -i 11 -n 1 -opt 0x52,0x6,0x5,0x4,0xc0,0xa8,0x64,0x0 -r 172.16.255.1 -s 10.0.0.100 -a

main(): Relay IPv4 address 172.16.255.1 was successfully added.

main(): waiting till RelayAddr=172.16.255.1 is reachabled

DHCPRawClient::DhcpClient() CLient:0 is starting

LeaseGranted:

        ClientID:0

        MyIP:192.168.100.60

        ServerIP:10.0.0.100
        
        LeaseObtened:Thu May 21 22:08:05 2020
        
        T1:Thu May 21 22:09:05 2020
        
        T2:Thu May 21 22:09:50 2020

DHCPRawClient::DhcpClient(): CLient:0 will send DHCPRelease in 10 secs.
`
 # Author : 
 vincent.douhet@gmail.com / vidou@microsoft.com
