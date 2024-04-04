# Projects
Establishing Connections
Produce a script or series of scripts to demonstrate both secure and insecure remote 
connections to a network device within your topology. This script should provide the 
following capability:
1. Insecure remote connection to router or switch device(s) within the topology 
2. Secure remote connection to routing device(s) within the topology 
3. Backup of router or switch device configuration to a remote machine
CI/CD Delivery 1 – create a script or series of scripts to achieve the above and 
submit to Moodle. (10%) 
2. Networking Device Comparison
Produce, or include within your existing work from Delivery 1, a script to compare the 
configuration of a network device. Your script should provide the following capability:
1. Compare the current running configuration of a network device with the startup configuration
2. Compare the current running configuration of a network device with a local 
offline version stored on a remote machine
CI/CD Delivery 2 – create a small script to achieve the above and submit to Moodle.
(15%) 
5
3. Remote device configuration
Produce, or include within your existing work, a script to configure at least one of the 
following options:
• Configure a loopback and appropriate IP address on a router within the 
topology
• Configure at least one of the following protocols on a network device within 
the topology and advertise appropriately: OSPF/EIGRP/RIP. You should use 
the knowledge gained from CMP5320 Networking Technologies to inform your 
configuration decisions
• Simultaneous or sequential configuration of at least two network devices, with 
appropriate VLAN configurations deployed


PART 1

#import required modlues/packages/library
import pexpect

#define variables
ip_address = '192.168.56.101'
username = 'devnet'
password = 'devnetadmin'

#create telnet session
session = pexpect.spawn('telnet ' + ip_address, encoding='utf-8', timeout=20)
result = session.expect(['username:', pexpect.timeout])
session.sendline(username)
result = session.expect(['password:', pexpect.timeout])


#check for error, if exists then display error and exit
if result != 0:
    print('---error" creating session for:', ip_address)
    exit()

#session is expecting username, enter details
#check for error, if existts then display error and exit
if result !=0:
    print('----failure! entering username:', username)
    exit()

#session is expecting password, enter details
session.sendline(password)
result = session.expect(['#', pexpect.timeout])

#check for error, if exists then display error and exit
if result != 0:
    print('--- error! entering password: ', password)
    exit()

#display a success message if it works
print('-------------------------------------')
print('')
print('-----success! connecting to: ', ip_address)
print('----------- username:', username)
print('----------- password:', password)
print('')
print('-------------------------------------')
session.close






#import required modlues/packages/library
import pexpect

#define variables
ip_address = '192.168.56.101'
username = 'devnet'
password = 'devnetadmin'
password_enable = 'devnetclass'
#create the ssh session
session = pexpect.spawn('ssh ' + username + '@' + ip_address, encoding='utf-8', timeout=20)
result = session.expect(['password:', pexpect.timeout, pexpect.eof])

#check for error, if exits then display error and exit
if result != 0:
    print('----eerror! creating session for:', ip_address)
    exit()

#session expecting password, enter details
session.sendline(password)
result = session.expect(['>', pexpect.tiemout, pexpect.eof])

#check for error, if exists then dusplay error and exit
if result != 0:
    print('----error! entering password:', password)
    exit()

#enter enable mode
session.sendline('enable')
result = session.expect(['password:', pexpect.timeout, pexpect.eof])

#check for error, if exists then dusplay error and exit
if result != 0:
    print('----error! entering enable mode')
    exit()

#send enable password details
session.sendline(password_enable)
result = session.expect(['#', pexpect.timeout, pexpect.eof])

#check for error, if exists then dusplay error and exit
if result != 0:
    print('---error! entering enable mode after sending password')
    exit()

#enter configuration mode
session.sendline('configure ternminal')
result = session.expect([r'.\(config\)#', pexpect.timeout, pexpect.eof])

#check for error, if exists then display erroe and exit
if result != 0:
    print('---- error! entering config mode')
    exit()

#change hostname to r1
session.sendline('hostname r1')
result = session.expect([r'r1\(config\)#', pexpect.timeout, pexpect.eof])

#check for error, if exists then display erroe and exit
if result != 0:
    print('--- error setting hostname')

    #exit config mode
    session.sendline('exit')
    #exit enable mode
    session.sendline('exit')

#display a success message if works
print('----------------------------------')
print('')
print('---success! connecting to: ', ip_address)
print('----- username: ', username)
print('------ password:', password)
print('')
print('----------------------------------')

session.close













