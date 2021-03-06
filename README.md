# ns_ddns
Dynamic DNS record update with NameSilo. OpenVPN version.


This is a Bash script that will update Namesilo's DNS record when a host IP address has changed, so long as OpenVPN is not running. Set this script to run as cronjob in your system for automated updates.

Tested in Fedora 23, CentOS 7, and Ubuntu 14.04+.
## Prerequisites:

    Generate API key in the “api manager” at Namesilo

    Make sure your system have command dig and xmllint. If not, install them:

on CentOS:

sudo yum install bind-utils libxml2

on Ubuntu/Debian:

sudo apt-get install dnsutils libxml2-utils
## How to use:

    Download and save the Bash script.
    Modify the script, set “DOMAINS” and “APIKEY” at the beginning of the script.
    Set file permission to make it executable.
    Create cronjob (optional):
        */30 * * * * bash /path/to/ns_ddns.sh >/dev/null 2>&1

## Manual test:

You should test the script to verify that actually can update the DNS record at Namesilo.

Step 1: Create an A record in DNS Manager at Namesilo. Set it to a random IP address (not the same public IP of yours). For example:

test.mydomain.tld A 1.2.3.4

Step 2: Run the script to try to update this DNS record

Step 3: Verify:

dig +short test.domain.tld @ns1.dnsowl.com

(you may also try other DNS server at Namesilo, e.g. ns2.dnsowl.com， ns3.dnsowl.com )

The result should show updated DNS record with your current public IP address. (Note: DNS record update need time to propagate to other DNS server, so if your check against other DNS server you may not see the update right away.)
