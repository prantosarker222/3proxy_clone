# 3APA3A 3proxy tiny proxy server
(c) 2002-2019 by Vladimir '3APA3A' Dubrovin <3proxy@3proxy.ru>


## Download: 
	https://github.com/z3APA3A/3proxy/releases
	or
	https://3proxy.org/download/
Archive of old versions: https://github.com/z3APA3A/3proxy-archive

## Setup

`3proxy --install`
	
installs and starts proxy as Windows service
(config file should be located in the same directory)


`3proxy --remove`

removes the service (should be stopped before via
'net stop 3proxy').

To build in Linux install git and build-essential packages, use

git clone https://github.com/z3apa3a/3proxy
cd 3proxy
ln -s Makefile.Linux Makefile
make
sudo make install

use /etc/3proxy/add3proxyuser.sh script to add users.



Please read doc/html/index.html and man pages.


## Features:
  1. General
	+ IPv6 support for incoming and outgoing connection,
	  can be used as a proxy between IPv4 and IPv6 networks
	  in either direction.
	+ HTTP/1.1 Proxy with keep-alive client and server support,
          transparent proxy support.
	+ HTTPS (CONNECT) proxy (compatible with HTTP/2 / SPDY)
	+ Anonymous and random client IP emulation for HTTP proxy mode
	+ FTP over HTTP support.
	+ DNS caching with built-in resolver
	+ DNS proxy
	+ DNS over TCP support, redirecting DNS traffic via parent
	  proxy
	+ SOCKSv4/4.5 Proxy
	+ SOCKSv5 Proxy
	+ SOCKSv5 UDP and BIND support (fully compatible with
	  SocksCAP/FreeCAP for UDP)
	+ Transparent SOCKS redirection for HTTP, POP3, FTP, SMTP
	+ POP3 Proxy
	+ FTP proxy
	+ TCP port mapper (port forwarding)
	+ UDP port mapper (port forwarding)
	+ SMTP proxy
	+ Threaded application (no child process).
	+ Web administration and statistics
	+ Plugins for functionality extension
	+ Native 64 bit application
  2. Proxy chaining and network connections
	+ Can be used as a bridge between client and different proxy type
	  (e.g. convert incoming HTTP proxy request from client to SOCKSv5
	  request to parent server).
	+ Connect back proxy support to bypass firewalls
	+ Parent proxy support for any type of incoming connection
	+ Username/password authentication for parent proxy(s).
	+ HTTPS/SOCKS4/SOCKS5 and ip/port redirection parent support
	+ Random parent selection
	+ Chain building (multihop proxing)
	+ Load balancing between few network connections by choosing network
	  interface
  3. Logging
	+ tuneable log format compatible with any log parser
	+ stdout logging
	+ file logging
	+ syslog logging (Unix)
	+ ODBC logging
	+ RADIUS accounting
	+ log file rotation (hourly, daily, weekly, monthly)
	+ automatic log file comperssion with external archiver (for files)
	+ automatic removal of older log files
	+ Character filtering for log files
	+ different log files for different servces are supported
  4. Access control
	+ ACL-driven Access control by username, source IP,
	destination IP/hostname, destination port and destination action
	(POST, PUT, GET, etc), weekday and daytime.
	+ ACL-driven (user/source/destination/protocol/weekday/daytime or
	combined) bandwith limitation for incoming and (!)outgoing trafic.
	+ ACL-driven (user/source/destination/protocol/weekday/daytime or
	combined) traffic limitation per day, week or month for incoming and
	outgoing traffic
	+ User authentication by username / password
	+ RADIUS Authentication and Authorization
	+ User authentication by DNS hostname
	+ Access control by username/password for SOCKSv5 and HTTP/HTTPS/FTP
	+ Cleartext or encrypted (crypt/MD5 or NT) passwords.
	+ Connection redirection
	+ Access control by requested action (CONNECT/BIND, 
	  HTTP GET/POST/PUT/HEAD/OTHER).
	+ All access control entries now support weekday and time limitations
	+ Hostnames and * templates are supported instead of IP address
  5. Extensions
	+ Regular expression filtering (with PCRE) via PCREPlugin
	+ Authentication with Windows username/password (cleartext only)
	+ SSL/TLS decryptions with certificate spoofing
	+ Transparent redirection support for Linux and *BSD
  6. Configuration
	+ support for configuration files
	+ support for includes in configuration files
	+ interface binding
	+ socket options
	+ running as daemon process
	+ utility for automated networks list building
	+ configuration reload on any file change
     Unix
	+ support for chroot
	+ support for setgid
	+ support for setuid
	+ support for signals (SIGUSR1 to reload configuration)
     Windows
	+ support --install as service
	+ support --remove as service
	+ support for service START, STOP, PAUSE and CONTINUE commands (on
	PAUSE no new connection accepted, but active connections still in
	progress, on CONTINUE configuration is reloaded)
     Windows 95/98/ME
	+ support --install as service
	+ support --remove as service
  6. Compilation
	+ MSVC (static)
	+ OpenWatcom (static)
	+ Intel Windows Compiler (msvcrt.dll)
	+ Windows/gcc (msvcrt.dll)
	+ Cygwin/gcc (cygwin.dll)
	+ Unix/gcc
	+ Unix/ccc
	+ Solaris
	+ Mac OS X, iPhone OS
	+ Linux and derivered systems
	+ Lite version for Windows 95/98/NT/2000/XP/2003
	+ 32 bit and 64 bit versions for Windows Vista and above, Windows 2008 server and above 

3proxy    	Combined proxy server may be used as
		executable or service (supports installation and removal).
		It uses config file to read it's configuration (see
		3proxy.cfg.sample for details).
		3proxy.exe is all-in-one, it doesn't require all others .exe
		to work.
		See 3proxy.cfg.sample for examples, see man 3proxy.cfg

proxy    	HTTP proxy server, binds to port 3128
ftppr    	FTP proxy server, binds to port 21
socks    	SOCKS 4/5 proxy server, binds to port 1080
ftppr		FTP proxy server, please do not mess it with FTP over HTTP
		proxy used in browsers
pop3p    	POP3 proxy server, binds to port 110. You must specify
		POP3 username as username@target.host.ip[:port]
		port is 110 by default.
		Exmple: in Username configuration for you e-mail reader
		set someuser@pop.example.org, to obtains mail for someuser
		from pop.somehost.ru via proxy.
smtpp    	SMTP proxy server, binds to port 25. You must specify
		SMTP username as username@target.host.ip[:port]
		port is 25 by default.
		Exmple: in Username configuration for you e-mail reader
		set someuser@mail.example.org, to send mail as someuser
		via mail.somehost.ru via proxy.
tcppm    	TCP port mapping. Maps some TCP port on local machine to
		TCP port on remote host.
udppm    	UDP port mapping. Maps some UDP port on local machine to
		UDP port on remote machine. Only one user simulationeously
		can use UDP mapping, so it cann't be used for public service
		in large networks. It's OK to use it to map to DNS server
		in small network or to map Counter-Strike server for single
		client (you can use few mappings on different ports for
		different clients in last case).
mycrypt    	Program to obtain crypted password fro cleartext. Supports
		both MD5/crypt and NT password.
			mycrypt password
		produces NT password
			mycrypt salt password
		produces MD5/crypt password with salt "salt".
dighosts    	Utility for building networks list from web page.


Run utility with --help option for command line reference.


## Latest version is available from :
https://3proxy.org/


## Want to donate the project? 
https://3proxy.org/donations/
