# dnssec_dns_server_test

A script to test A records from a zone where DNSSEC is enabled using a list of DNS servers.

## Usage
```
./delv_dnssec [-f <dns-server-txt-file> -u <fqdn-to-check-dnssec>]

-f	--file		 Hand over path to DNS Server file fomratted in 2 rows e.g. Vodafone_Munich 141.1.27.249. Mandatory
-r	--repeat	 Set the number of repetitions, how often a single query should be repeated when first try fails to resolve. Default 3.
			 Increases the reliability of queries. Must be at least 1.
-t	--testquery	 Test query to test if DNS server IP is able to resolve something - default is google.com
-u	--url		 DNSSEC A record FQDN from DNSSEC domain you want to verify if DNS server can resolve DNSSEC - e.g. dnssec.com (A record) - Mandatory
-d	--timedistance	 Set the time interval between each DNSSEC query from the DNS server list in seconds. Default 3 seconds.
```

Example with all parameters:
```
./dnssec_dns_server_test -f ~/dns_server.txt -u dnssec.com -t amazon.com -r 5 -d 2
Google_Public 8.8.8.8; Successful: amazon.com; Successful: dnssec.com; DNSSEC supported; Fully validated
Cloudflare 1.1.1.1; Successful: amazon.com; Successful: dnssec.com; DNSSEC supported; Fully validated
OpenDNS 208.67.222.222; Successful: amazon.com; Successful: dnssec.com; DNSSEC supported; Fully validated
CyberGhost 38.132.106.139; Successful: amazon.com; Successful: dnssec.com; DNSSEC supported; Fully validated
Hagenberg 193.186.170.50; Successful: google.com; Successful: test.awin-dnssec.com; DNSSEC not supported
```

## Considerations
- Make sure the DNS server list has only two columns 1. name 2. ip address. The name can be set as desired but without empty spaces.
- DNS server file can be handed over while using absolute or absolute path.
- It can only one A record tested at once.  