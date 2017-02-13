

Skip to content
This repository

    Pull requests
    Issues
    Gist

    @robisys

3,133
39,632

    11,894

docker/docker
Code
Issues 2,098
Pull requests 157
Projects 3
Wiki
Pulse
Graphs
Docker should use the host network DNS server #23910
Closed
nottrobin opened this Issue on 23 Jun 2016 · 22 comments
Assignees
No one assigned
Labels
area/networking
version/1.11
Projects
None yet
Milestone
 
1.14.0
Notifications

You’re not receiving notifications from this thread.
16 participants
@nottrobin
@nathanleclaire
@cpuguy83
@ovidiub13
@iflowfor8hours
@justincormack
@awilkins
@iraadit
@bsingr
@krak3n
@sanimej
@butlermd
@dqminh
@setiseta
@GordonTheTurtle
@thaJeztah
@nottrobin
nottrobin commented on 23 Jun 2016 • edited
Summary

In networks where external DNS servers are blocked, Docker containers running on Ubuntu hosts can't resolve DNS at all because they are trying to use 8.8.8.8 as their DNS server. Docker should detect the network DNS server.
Detail

When spinning up a container, Docker will by default check for a DNS server defined in /etc/resolv.conf in the host OS, and if it doesn't find one, or finds only 127.0.0.1, will opt to use Google's public DNS server 8.8.8.8.

My development machine is running Ubuntu 16.04 which uses dnsmasq by default, so /etc/resolv.conf is always set to 127.0.0.1, even though it is usually actually getting its DNS settings from whatever network its connected to:

$ cat /etc/resolv.conf | grep nameserver  # What Docker sees
nameserver 127.0.1.1
$ nmcli dev show | grep IP4.DNS  # My actual DNS server
IP4.DNS[1]:                             10.1.1.3

and so Docker containers always default to using 8.8.8.8 rather than using the same DNS server as the host OS.

In my office network external DNS servers are blocked, and so me and my whole team are finding docker containers failing with obscure errors which result from failing to resolve DNS.

There is a workaround, which I help walk all my team members through so they can still use Docker. Although it's frustrating that whenever Docker gets updated, it seems the daemon config file is overwritten and we have to implement the fix all over again. This is less of a problem for me, but is causing significant trouble for our less systems-focused developers.

Is there any hope that Docker might be able to intelligently pick up the network's DNS server in the future?
Steps to reproduce the issue

    Use a host OS that makes use of dnsmasq (e.g. Ubuntu since 12.04)
    Connect to a network that blocks access to external DNS servers like 8.8.8.8
    Try to resolve DNS with Docker (docker run busybox nslookup google.com)

What I get

$ docker run busybox nslookup google.com
Server:    8.8.8.8
Address 1: 8.8.8.8

nslookup: can't resolve 'google.com'

What I expected

$ docker run busybox nslookup google.com
Server:    10.1.1.3
Address 1: 10.1.1.3

Name:      google.com
Address 1: 2a00:1450:4009:811::200e lhr26s02-in-x200e.1e100.net
Address 2: 216.58.198.174 lhr25s10-in-f14.1e100.net

System information

I'm running Xenial natively on a Dell XPS 13 9350.

$ cat /etc/os-release 
NAME="Ubuntu"
VERSION="16.04 LTS (Xenial Xerus)"
ID=ubuntu
ID_LIKE=debian
PRETTY_NAME="Ubuntu 16.04 LTS"
VERSION_ID="16.04"
HOME_URL="http://www.ubuntu.com/"
SUPPORT_URL="http://help.ubuntu.com/"
BUG_REPORT_URL="http://bugs.launchpad.net/ubuntu/"
UBUNTU_CODENAME=xenial

$ docker version
Client:
 Version:      1.11.1
 API version:  1.23
 Go version:   go1.5.4
 Git commit:   5604cbe
 Built:        Tue Apr 26 23:43:49 2016
 OS/Arch:      linux/amd64

Server:
 Version:      1.11.1
 API version:  1.23
 Go version:   go1.5.4
 Git commit:   5604cbe
 Built:        Tue Apr 26 23:43:49 2016
 OS/Arch:      linux/amd64

$ docker info
Containers: 61
 Running: 3
 Paused: 0
 Stopped: 58
Images: 421
Server Version: 1.11.1
Storage Driver: aufs
 Root Dir: /var/lib/docker/aufs
 Backing Filesystem: extfs
 Dirs: 441
 Dirperm1 Supported: true
Logging Driver: json-file
Cgroup Driver: cgroupfs
Plugins: 
 Volume: local
 Network: bridge null host
Kernel Version: 4.4.0-24-generic
Operating System: Ubuntu 16.04 LTS
OSType: linux
Architecture: x86_64
CPUs: 4
Total Memory: 15.54 GiB
Name: xps
ID: G4MN:GTXD:4KZP:PTZC:DBYK:WOLA:R3GF:TKLW:ZOOX:NXZT:ALNG:F22D
Docker Root Dir: /var/lib/docker
Debug mode (client): false
Debug mode (server): false
Username: nottrobin
Registry: https://index.docker.io/v1/
WARNING: No swap limit support

@GordonTheTurtle GordonTheTurtle added the version/1.11 label on 23 Jun 2016
@nathanleclaire
Contributor
nathanleclaire commented on 23 Jun 2016

@mavenugo @mrjana FYI
@cpuguy83
Contributor
cpuguy83 commented on 24 Jun 2016

The systemd unit file should not be edited directly.
Systemd has a facility called "drop-ins" that allow you to override/augment the unit file.
https://docs.docker.com/engine/admin/systemd/

In addition, it would probably be best to configure the docker daemon via it's config file rather than the systemd unit file. By default docker reads config from /etc/docker/daemon.json. https://docs.docker.com/engine/reference/commandline/dockerd/#linux-configuration-file
@nottrobin
nottrobin commented on 24 Jun 2016

Ah! Wonderful suggestions. Thanks @cpuguy83, I'll update my blog post.
@ovidiub13
ovidiub13 commented on 30 Jun 2016

I've solved this by adding a daemon configuration file. But I would sure love for this to be implemented.
@thaJeztah thaJeztah added the group/networking label on 1 Jul 2016
@iflowfor8hours
iflowfor8hours commented on 20 Aug 2016

@cpuguy83 Nice one, I didn't know about the /etc/docker/daemon.json. Might that file get created in a default install to signal to users this is where configuration should live? I went straight for the systemd drop-ins.
@justincormack
Member
justincormack commented on 20 Aug 2016

It is not very easy to implement this as docker has no way to know the
upstream servers. If you set your local DNS relay on localhost to also
listen on the docker0 IP and put that address in resolv.conf that would
also work.

On 30 Jun 2016 3:12 p.m., "Ovidiu-Florin BOGDAN" notifications@github.com
wrote:

I've solved this by adding a daemon configuration file. But I would sure
love for this to be implemented.

—
You are receiving this because you are subscribed to this thread.
Reply to this email directly, view it on GitHub
#23910 (comment), or mute
the thread
https://github.com/notifications/unsubscribe/AAdcPFlthUzL2cze4iV_wGe0xRFhQPRpks5qQ87WgaJpZM4I9Lm8
.
@nottrobin
nottrobin commented on 9 Sep 2016

@justincormack I can discover the DNS servers by doing nmcli dev show | grep DNS. Couldn't docker do something similar? I mean, more generally, if the system knows its DNS servers (which it must) then surely docker can discover them somehow.
@awilkins
awilkins commented on 19 Sep 2016 • edited

On Ubuntu, I settled on doing this ( as @justincormack describes) by...

    Adding a /etc/docker/daemon.json that passed in the docker0 bridge IP as a DNS server
    Adding a /etc/NetworkManager/dnsmasq.d/docker-bridge.conf file that directs the NM-managed DNS cache to listen to the docker0 bridge IP as well as 127.0.1.1

Now container DNS lookups go through your local dnsmasq instance, so DNS in the container should work just as well as DNS on the host.

@nottrobin - my problem specifically was that my system did know it's DNS servers and was passing them to the container - but because those servers were on a VPN, there was no route to them from inside the container, hence all DNS lookups failed. This was partly down to the non-NetworkManager based VPN client we're using that overwites resolv.conf. Turned that "feature" off and instead added config for that subdomain on NetworkManager's dnsmasq itself.
@justincormack
Member
justincormack commented on 20 Sep 2016

@nottrobin nmcli only applies to systems running NetworkManager, there is not an equivalent for other setups.
@thaJeztah thaJeztah referenced this issue on 21 Sep 2016
Closed
Containers cannot resolve DNS if docker host uses 127.0.0.1 as resolver #541
@iraadit
iraadit commented on 10 Oct 2016

Thank you A LOT for the workaround @nottrobin, working great even when doing "docker build"
It had been three days of looking for a solution without success before finding your post
This was referenced on 14 Nov 2016
Open
docker clear-datacenter/plan#4
Open
GELF Driver only does DNS resolution on startup #17904
@bsingr
bsingr commented on 23 Nov 2016 • edited

Your solution works @awilkins.

Additionally it requires to allow port 53 traffic on the ubuntu firewall for the docker0 bridge ip.

Quick test: disable the ubuntu firewall completely with sudo ufw disable
@krak3n
krak3n commented on 1 Dec 2016

@bsingr what rule did you use? I've tried loads and can't get it to work on Ubuntu 16.04 - i've resorted to host network mode 😭
This was referenced on 2 Dec 2016
Closed
Cannot update plugins when using docker-compose SonarSource/docker-sonarqube#55
Merged
Add support in embedded DNS server for host loopback resolver docker/libnetwork#1595
@sanimej
Contributor
sanimej commented on 19 Dec 2016

@nottrobin Instead of trying to detect the external resolver used by the host resolver the better approach is to allow the containers' DNS queries to be forwarded to the host resolver if the resolv.conf has a loopback address. Using the host resolver has other use cases as well. Its doable with the docker embedded DNS server which is used by default for user defined networks. I pushed a PR in libnetwork for this.
@butlermd
butlermd commented on 9 Jan

@awilkins or @bsingr, do either of you have more details about how you configured docker-bridge.conf? The daemon.json file seems like it should be simple enough:

{
  "dns": [
    "172.17.0.1"
  ]
}

But I'm unclear on how you configured dnsmasq.
@awilkins
awilkins commented on 9 Jan • edited

On ubuntu, add a file /etc/NetworkManager/dnsmasq.d/docker-bridge.conf

listen-address=172.17.0.1

By default it only listens to DNS requests from 127.0.0.1 (ie, your computer). This tells it to listen to the docker bridge also.
@butlermd
butlermd commented on 9 Jan

@awilkins Thanks for the clarification!
@awilkins
awilkins commented on 9 Jan • edited

Also looks like a PR with support for doing this less cryptically landed a few days ago in libnetwork

AFAIK though this won't work for the docker0 network bridge.

docker/libnetwork@1ed42d1
@sanimej
Contributor
sanimej commented on 9 Jan

@awilkins Yes, it doesn't work for docker0 bridge because the Docker DNS server is used only for the user created networks. The fix to forward the queries to host loopback resolver relies on the embedded DNS server.
@sanimej sanimej referenced this issue on 9 Jan
Merged
vendorin libnetwork @f9fa6e0 #29891
@thaJeztah thaJeztah closed this in #29891 on 11 Jan
@thaJeztah thaJeztah added this to the 1.14.0 milestone on 11 Jan
@vga101 vga101 referenced this issue in mayflower/docker-ls on 13 Jan
Closed
Local name servers are not used #18
@dqminh
Contributor
dqminh commented 28 days ago

@sanimej just to make sure i understand the patch correctly, it only allows docker embedded DNS server to forward queries to the local nameserver ?

We are using https://github.com/gliderlabs/hostlocal, which will still be required if we dont want to use docker embedded DNS server, is that correct ?
@sanimej
Contributor
sanimej commented 27 days ago

@dqminh Yes, this patch essentially differentiates between loopback IP in the container namespace vs host namespace. This allows the embedded DNS server to forward the queries appropriately. From a quick glance it looks like hostlocal package is intended to be used with containers in net=host mode. This patch is not relevant in that case.
@dqminh
Contributor
dqminh commented 27 days ago

@sanimej i think hostlocal should work in bridge mode as well since it adds a route in the host. Thanks for the confimation about the embedded DNS server.
@setiseta
setiseta commented 14 days ago

hm, just to ask, is it possible to setup a dnsmasq in a container as default dns for other dockers in any way?
i just cant find a description about this on the internet.
is this not possible?
@robisys

Attach files by dragging & dropping,

, or pasting from the clipboard.
Styling with Markdown is supported

    Contact GitHub API Training Shop Blog About 

    © 2017 GitHub, Inc. Terms Privacy Security Status Help 

