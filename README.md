# Setup Clickhouse-Server in Ubuntu 16.04 WSL
Tutorial to setup Clickhouse in Ubuntu - WSL
## Ubuntu 16.04 installation

If you have Ubuntu 16.04 in Window 10, you could skip this step. Or not, you need to enable the WSL (Windows Subsystem Linux ) feature.

Open PowerShell Run as Administrator and run this code :

    Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux

Then you get **Ubuntu 16.04** in Window Store :
[Ubuntu 16.04](https://www.microsoft.com/en-us/p/ubuntu-1604-lts/9pjn388hp8c9)

## ClickHouse installation

Add the repository which ClickHouse will be downloaded:

    sudo apt-add-repository "deb http://repo.yandex.ru/clickhouse/deb/stable/ main/"

Then launch the setup process (it takes several minutes):

    sudo apt-key adv --keyserver keyserver.ubuntu.com --recv E0C56BD4 # optional  
    sudo apt-get update  
    sudo apt-get install clickhouse-client clickhouse-server

To start/restart/stop the server, run:

    sudo service clickhouse-server start/restart/stop

The setup is complete. To make sure it was successful, launch the console client:

    clickhouse-client    
Your screen should be like that

    {host_name}:~$ clickhouse-client
    ClickHouse client version 19.9.2.4 (official build).
    Connecting to localhost:9000 as user default.
    Connected to ClickHouse server version 19.9.2 revision 54421.
    
    {host_name}.localdomain :)

## Troubleshooting

If you have issue like this want

    clickhouse-client
    ClickHouse client version 1.1.54383.
    Connecting to localhost:9000.
    Code: 102. DB::NetException: Unexpected packet from server localhost:9000, ::1 (expected Hello or Exception, got Unknown packet)

Please add the create a new config file in this folder:

    /etc/clickhouse-server/config.d/config.xml

    <?xml version="1.0"?>
    <yandex>
        <listen_host>::1</listen_host>
        <listen_host>127.0.0.1</listen_host>
    </yandex>

You are good to go!
