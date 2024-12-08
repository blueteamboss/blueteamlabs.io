# Resources
Find where to get licensing, free-shit, and learn!

## Log Solutions and SIEM
### Splunk
Splunk has the Splunk Developer program, which gives you a renewable 6-month Enterprise license

* 10GB/ingest a day
* Full Enterprise Usability
* Can deploy multiple servers

[Register for Splunk Developer](https://dev.splunk.com/enterprise/dev_license/)

Splunk may require you to prove developer usage, but in talking with Splunk reps (we invested heavily in Splunk as work) this is fairly lenient. I do have some concerns about how this changes under Cisco's leadership. Cisco does have a tendency to switch things up for no particular reason.

### Graylog
Graylog is one I've personally used in the past. It used to be called Graylog community, but is now Graylog open. It's a fantastic started log management/SIEM solution that atleast used to have alot of good pre-built security focused dashboards.
It's free and unlimited ingest.

[Download Graylog Open](https://graylog.org/downloads/)


### Elastic, Logstash, Kibana
Honestly, I wouldn't recommend this one personnally. While it does have widespread adoption in the larger data analytics and business intelligence space, for security there are far better pre-packaged, less labor intesive solutions. It does have an "on-prem/self-hosted" variant that can get you ingesting data and analyzing it, but much of the "security" features are locked behind paywalls and will need to be manually built out. Plus, its really a beast to manage if you intend to run it for any prolonged period of time.

[Get Elastic](https://www.elastic.co/downloads)

### Security Onion
Security Onion is pretty much the swiss-army knife. Combining the Elastic stack, Snort, open source 'EDR', and a ton of other things, its a good starting point for anyone learning how to ingest, analyze, and managem security logs for the security investigations, forsenics, and detection purposes. I've used it on and off for nearly as long as I can remember, and it's come a long way and is much more polished, stable, and stupid simple to deploy these days.

[Get SecurityOnion](https://github.com/Security-Onion-Solutions/securityonion/blob/2.4/main/DOWNLOAD_AND_VERIFY_ISO.md)'

### Wazuh
Wazuh is another great one, built again on the Elastic Stack. Notice a trend here? Alot of these have the Elastic stack under-the-hood, but are prepackaged versions with everything you would need to get up and running quick for a down and dirty security operations or engineering lab. I've used Wazuh before in my Homelab, and am looking to deploy it again soon, so maybe you'll get some additional coverage on that. I do need something that can provide endpoint security, as I'm currently ending the term with my current EDR solution. Free licenses only last so long I guess.

[Get Wazuh](https://wazuh.com/)

## Virtualization
### Proxmox VE
Proxmox VE is what I'm currently using for my homelab. It offers much the same featurset you'd expect from you typic HCI hypervisor, but without the BS of greedy vendors switching up licensing and making it harder to learn or obtain experience. PVE is free in the sense that you won't get access to production quality stable updates and patches. You'll be stuck with whatevers in the debian repository and their non-production repos.

[Download Proxmox](https://www.proxmox.com/en/downloads)

### XCP-ngg
XCP-ng is one I haven't personally used extensively, but is another great alternative for virtualizing your homelab. Again, another does what you'd expect. There are some oddities and additional things required to get clustering working, atleast when I tried it around 2-years ago, but it definitely is a good alternative if you're looking for something that'll provide the same functionality as VMWare, but are interested in learning something other than Proxmox.

[Download XCP-ng](https://xcp-ng.org/#easy-to-install)

## Linux KVM/QEMU with virt-manager
This one is good if you're a heavy linux user and just want to run raw KVM and QEMU. It's something I personally do for my desktop, as I virtualize a Windows box for the occasional gaming/video editing session. Still not many good alternatives for AAA gaming or content editing on Linux. Sure, Proton has come a long way, but it certainly isn't perfect, not to mention wayland support for NVIDIA GPUs has been....lackluster. 

Anyway, if you're looking something free that you can just install on your linux box, you can use virt-manager to get you along.

[Learn about virt-manager](https://virt-manager.org/)