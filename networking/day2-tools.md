# Day 2 — Networking Tools (Debian)

## Evidence

### ip a
```text
1: lo: <LOOPBACK,UP,LOWER_UP> ...
    inet 127.0.0.1/8 scope host lo
    inet6 ::1/128 scope host

2: enp60s0: <NO-CARRIER,BROADCAST,MULTICAST,UP> ... state DOWN
    link/ether a4:4c:c8:01:bb:c2

3: wlp61s0: <BROADCAST,MULTICAST,UP,LOWER_UP> ... state UP
    inet 192.168.0.9/24 ... wlp61s0
    inet6 2804:.../64 scope global dynamic
    inet6 fe80::.../64 scope link

4: tailscale0: <POINTOPOINT,...,UP,LOWER_UP> ...
    inet 100.71.140.125/32 scope global tailscale0

5: docker0: <NO-CARRIER,BROADCAST,MULTICAST,UP> ... state DOWN
    inet 172.17.0.1/16 scope global docker0


### ip r

default via 192.168.0.1 dev wlp61s0 proto dhcp src 192.168.0.9 metric 600 
172.17.0.0/16 dev docker0 proto kernel scope link src 172.17.0.1 linkdown 
192.168.0.0/24 dev wlp61s0 proto kernel scope link src 192.168.0.9 metric 600 

### ss -tulpn
Netid   State    Recv-Q   Send-Q                           Local Address:Port           Peer Address:Port        Process                                        
udp     UNCONN   0        0                                      0.0.0.0:52167               0.0.0.0:*            users:(("kdeconnectd",pid=5025,fd=23))        
udp     UNCONN   0        0                                      0.0.0.0:52552               0.0.0.0:*            users:(("kdeconnectd",pid=5025,fd=29))        
udp     UNCONN   0        0                                  224.0.0.251:5353                0.0.0.0:*            users:(("chrome",pid=6662,fd=403))            
udp     UNCONN   0        0                                  224.0.0.251:5353                0.0.0.0:*            users:(("chrome",pid=6662,fd=402))            
udp     UNCONN   0        0                                  224.0.0.251:5353                0.0.0.0:*            users:(("chrome",pid=6710,fd=113))            
udp     UNCONN   0        0                                  224.0.0.251:5353                0.0.0.0:*            users:(("chrome",pid=6710,fd=53))             
udp     UNCONN   0        0                                      0.0.0.0:5353                0.0.0.0:*            users:(("kdeconnectd",pid=5025,fd=21))        
udp     UNCONN   0        0                                      0.0.0.0:5353                0.0.0.0:*                                                          
udp     UNCONN   0        0                                      0.0.0.0:56197               0.0.0.0:*            users:(("kdeconnectd",pid=5025,fd=26))        
udp     UNCONN   0        0                                      0.0.0.0:57345               0.0.0.0:*                                                          
udp     UNCONN   0        0                                      0.0.0.0:41641               0.0.0.0:*                                                          
udp     UNCONN   0        0                                            *:59530                     *:*            users:(("kdeconnectd",pid=5025,fd=27))        
udp     UNCONN   0        0                                            *:46132                     *:*            users:(("kdeconnectd",pid=5025,fd=25))        
udp     UNCONN   0        0          [fe80::ce2f:294c:8f42:7b37]%wlp61s0:546                    [::]:*                                                          
udp     UNCONN   0        0                                            *:34273                     *:*            users:(("kdeconnectd",pid=5025,fd=28))        
udp     UNCONN   0        0                                            *:1716                      *:*            users:(("kdeconnectd",pid=5025,fd=19))        
udp     UNCONN   0        0                                         [::]:52577                  [::]:*                                                          
udp     UNCONN   0        0                                            *:54203                     *:*            users:(("kdeconnectd",pid=5025,fd=24))        
udp     UNCONN   0        0                                         [::]:5353                   [::]:*                                                          
udp     UNCONN   0        0                                            *:5353                      *:*            users:(("kdeconnectd",pid=5025,fd=22))        
udp     UNCONN   0        0                                         [::]:41641                  [::]:*                                                          
tcp     LISTEN   0        500                                    0.0.0.0:8084                0.0.0.0:*                                                          
tcp     LISTEN   0        4096                                 127.0.0.1:11434               0.0.0.0:*                                                          
tcp     LISTEN   0        4096                            100.71.140.125:39057               0.0.0.0:*                                                          
tcp     LISTEN   0        5                                      0.0.0.0:4330                0.0.0.0:*                                                          
tcp     LISTEN   0        4096                                 127.0.0.1:631                 0.0.0.0:*                                                          
tcp     LISTEN   0        5                                      0.0.0.0:44321               0.0.0.0:*                                                          
tcp     LISTEN   0        128                                    0.0.0.0:44322               0.0.0.0:*                                                          
tcp     LISTEN   0        128                                    0.0.0.0:44323               0.0.0.0:*                                                          
tcp     LISTEN   0        128                                  127.0.0.1:5939                0.0.0.0:*                                                          
tcp     LISTEN   0        5                                         [::]:4330                   [::]:*                                                          
tcp     LISTEN   0        50                                           *:1716                      *:*            users:(("kdeconnectd",pid=5025,fd=20))        
tcp     LISTEN   0        511                                          *:80                        *:*                                                          
tcp     LISTEN   0        4096               [fd7a:115c:a1e0::2301:8c8a]:36444                  [::]:*                                                          
tcp     LISTEN   0        5                                         [::]:44321                  [::]:*                                                          
tcp     LISTEN   0        128                                       [::]:44322                  [::]:*                                                          
tcp     LISTEN   0        128                                       [::]:44323                  [::]:*                                                          
tcp     LISTEN   0        4096                                     [::1]:631                    [::]:*    


### dig github.com +short
4.228.31.150

### curl -I https://github.com
HTTP/2 200 
date: Sun, 11 Jan 2026 23:09:23 GMT
content-type: text/html; charset=utf-8
vary: X-PJAX, X-PJAX-Container, Turbo-Visit, Turbo-Frame, X-Requested-With, Accept-Language,Accept-Encoding, Accept, X-Requested-With
content-language: en-US
etag: W/"39164d05c73d09d78c24da4ee3c98428"
cache-control: max-age=0, private, must-revalidate
strict-transport-security: max-age=31536000; includeSubdomains; preload
x-frame-options: deny
x-content-type-options: nosniff
x-xss-protection: 0
referrer-policy: origin-when-cross-origin, strict-origin-when-cross-origin
content-security-policy: default-src 'none'; base-uri 'self'; child-src github.githubassets.com github.com/assets-cdn/worker/ github.com/assets/ gist.github.com/assets-cdn/worker/; connect-src 'self' uploads.github.com www.githubstatus.com collector.github.com raw.githubusercontent.com api.github.com github-cloud.s3.amazonaws.com github-production-repository-file-5c1aeb.s3.amazonaws.com github-production-upload-manifest-file-7fdce7.s3.amazonaws.com github-production-user-asset-6210df.s3.amazonaws.com *.rel.tunnels.api.visualstudio.com wss://*.rel.tunnels.api.visualstudio.com github.githubassets.com objects-origin.githubusercontent.com copilot-proxy.githubusercontent.com proxy.individual.githubcopilot.com proxy.business.githubcopilot.com proxy.enterprise.githubcopilot.com *.actions.githubusercontent.com wss://*.actions.githubusercontent.com productionresultssa0.blob.core.windows.net/ productionresultssa1.blob.core.windows.net/ productionresultssa2.blob.core.windows.net/ productionresultssa3.blob.core.windows.net/ productionresultssa4.blob.core.windows.net/ productionresultssa5.blob.core.windows.net/ productionresultssa6.blob.core.windows.net/ productionresultssa7.blob.core.windows.net/ productionresultssa8.blob.core.windows.net/ productionresultssa9.blob.core.windows.net/ productionresultssa10.blob.core.windows.net/ productionresultssa11.blob.core.windows.net/ productionresultssa12.blob.core.windows.net/ productionresultssa13.blob.core.windows.net/ productionresultssa14.blob.core.windows.net/ productionresultssa15.blob.core.windows.net/ productionresultssa16.blob.core.windows.net/ productionresultssa17.blob.core.windows.net/ productionresultssa18.blob.core.windows.net/ productionresultssa19.blob.core.windows.net/ github-production-repository-image-32fea6.s3.amazonaws.com github-production-release-asset-2e65be.s3.amazonaws.com insights.github.com wss://alive.github.com wss://alive-staging.github.com api.githubcopilot.com api.individual.githubcopilot.com api.business.githubcopilot.com api.enterprise.githubcopilot.com edge.fullstory.com rs.fullstory.com; font-src github.githubassets.com; form-action 'self' github.com gist.github.com copilot-workspace.githubnext.com objects-origin.githubusercontent.com; frame-ancestors 'none'; frame-src viewscreen.githubusercontent.com notebooks.githubusercontent.com www.youtube-nocookie.com; img-src 'self' data: blob: github.githubassets.com media.githubusercontent.com camo.githubusercontent.com identicons.github.com avatars.githubusercontent.com private-avatars.githubusercontent.com github-cloud.s3.amazonaws.com objects.githubusercontent.com release-assets.githubusercontent.com secured-user-images.githubusercontent.com/ user-images.githubusercontent.com/ private-user-images.githubusercontent.com opengraph.githubassets.com marketplace-screenshots.githubusercontent.com/ copilotprodattachments.blob.core.windows.net/github-production-copilot-attachments/ github-production-user-asset-6210df.s3.amazonaws.com customer-stories-feed.github.com spotlights-feed.github.com objects-origin.githubusercontent.com *.githubusercontent.com images.ctfassets.net/8aevphvgewt8/; manifest-src 'self'; media-src github.com user-images.githubusercontent.com/ secured-user-images.githubusercontent.com/ private-user-images.githubusercontent.com github-production-user-asset-6210df.s3.amazonaws.com gist.github.com github.githubassets.com assets.ctfassets.net/8aevphvgewt8/ videos.ctfassets.net/8aevphvgewt8/; script-src github.githubassets.com; style-src 'unsafe-inline' github.githubassets.com; upgrade-insecure-requests; worker-src github.githubassets.com github.com/assets-cdn/worker/ github.com/assets/ gist.github.com/assets-cdn/worker/
server: github.com
accept-ranges: bytes
set-cookie: _gh_sess=qRCOY7mzAdbjGTL3c7nOc0xv%2B1c2GIMDiEkHoZxhgVN2DtnCCbo0y98Exy5uut9MEetaKSPCLrlzxwe9HA7xeTcoKU7qAiaiZA4W9htxN39xSQnXjcWtjsPR8jkLSw%2BnMOSpDatXEyIX%2BDrr6juB8YR%2F2Vnt5%2BV37FjgYx%2BcYdi00se1WotycohDD93enwBnuW%2BR6%2Fda049vq%2Fo4xcRiosK%2BrZrj3NTK6Lc2u1O8Eq3nDi6qlT6rWBwLxuScmyeWwLqulc9KyEOIPm6gzzf8Ow%3D%3D--OV8yUcNU6By3MWC4--MPFh6NQgkXDspg%2FWpNX4Fw%3D%3D; Path=/; HttpOnly; Secure; SameSite=Lax
set-cookie: _octo=GH1.1.1765832638.1768172966; Path=/; Domain=github.com; Expires=Mon, 11 Jan 2027 23:09:26 GMT; Secure; SameSite=Lax
set-cookie: logged_in=no; Path=/; Domain=github.com; Expires=Mon, 11 Jan 2027 23:09:26 GMT; HttpOnly; Secure; SameSite=Lax
x-github-request-id: 6810:136E2F:3ED085F:48FE4B6:69642DA6



