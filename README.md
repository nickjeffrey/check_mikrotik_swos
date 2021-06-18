# check_mikrotik_swos
nagios check for MikroTik devices running SwitchOS (not RouterOS)

# Requirements
perl, snmpwalk, snmpget on nagios server
IP address configured on MikroTik device with SNMP enabled

# Configuration
You will need a section in the services.cfg file on the nagios server that looks similar to the following.
````
    # Define a service to check MikroTik devices running SwitchOL (not RouterOS)
    # Parameters are SNMP community name
    define service {
        use                             generic-service
        hostgroup_name                  all_mikrotik_swos
        service_description             MikroTik SwOS
        check_command                   check_mikrotik_swos!public
        }
````

You will need a section in the commands.cfg file on the nagios server that looks similar to the following.
````
# 'check_mikrotik_swos' command definition
    # parameters are -H hostname -C snmp_community
    define command{
        command_name    check_mikrotik_swos
        command_line    $USER1$/check_mikrotik_swos -H $HOSTADDRESS$ -C $ARG1$
        }
````

# Output
Output will look similar to the following:
````    
    MikroTik SwOS OK - CPU temperature:43.0C  Uptime:2 days Hostname:switch2 Model:CSS106-1G-4P-1S Firmware:SwOS v2.13  | cpu_temperature=43.0;65;60;; 
````
