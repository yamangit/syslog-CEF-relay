# syslog-CEF-relay
syslog formated log to CEF (RFC5424). It will conver the syslog default syslog formatted log to CEF (RFC 5424) log. 

# Instruaction and Information
|    S.N     | Container Name     | Purpose                |   Port     |  Protocol |
|----------- |--------------------|------------------------|------------|-----------|
| 1          |  relay             |   To convert default  syslog data to CEF |  20514     |  UDP/TCP  |                      
|------------|--------------------|------------------------|------------|-----------|
| 2          |   reciever         |   Enpoint where CEF log format is needed |  30514     |  UDP/TCP  |


### Clone the Repo

```bash
git clone https://github.com/yamangit/syslog-CEF-relay.git
cd syslog-CEF-relay
```
### Run the docker compose 
```bash
docker compose up -d
```
### To check docker status
```bash
docker ps

CONTAINER ID   IMAGE             COMMAND                  CREATED          STATUS          PORTS                                           NAMES
491613d1811e   syslog-reciever   "/usr/sbin/rsyslogd …"   30 seconds ago   Up 30 seconds   0.0.0.0:30514->30514/tcp, :::30514->30514/tcp   reciever
5698cff1480e   syslog-relay      "/usr/sbin/rsyslogd …"   29 seconds ago   Up 29 seconds   0.0.0.0:20514->20514/tcp, :::20514->20514/tcp   relay

```
### Go to the reciever container
```bash
docker exec -it reciever bash

root@491613d1811e:/#
```
### Run the tail command
```bash
root@491613d1811e:/# tail -f /var/log/syslog.cef.log
```
#### Output:
```bash
root@491613d1811e:/# tail -f /var/log/syslog.cef.log 
2024-04-18T22:57:43.131678+05:45 blink kernel CEF:0|kern|info|kernel| br-ce2e2d75e3ae: port 1(vethd47ebd2) entered blocking state
2024-04-18T22:57:43.131679+05:45 blink kernel CEF:0|kern|info|kernel| br-ce2e2d75e3ae: port 1(vethd47ebd2) entered forwarding state
2024-04-18T22:57:43.131679+05:45 blink kernel CEF:0|kern|info|kernel| br-ce2e2d75e3ae: port 1(vethd47ebd2) entered disabled state
2024-04-18T22:57:43.135648+05:45 blink kernel CEF:0|kern|info|kernel| br-ce2e2d75e3ae: port 2(veth1ba829f) entered disabled state
2024-04-18T22:57:43.135659+05:45 blink kernel CEF:0|kern|info|kernel| veth1ba829f: entered promiscuous mode
2024-04-18T22:57:43.335735+05:45 blink kernel CEF:0|kern|info|kernel| eth0: renamed from vethe5d938f
2024-04-18T22:57:43.407702+05:45 blink kernel CEF:0|kern|info|kernel| eth0: renamed from veth7a660ef
2024-04-18T22:57:43.443640+05:45 blink kernel CEF:0|kern|info|kernel| br-ce2e2d75e3ae: port 1(vethd47ebd2) entered forwarding state
2024-04-18T22:57:43.443649+05:45 blink kernel CEF:0|kern|info|kernel| br-ce2e2d75e3ae: port 2(veth1ba829f) entered forwarding state
2024-04-18T22:58:06.244503+05:45 blink rsyslogd-2359 CEF:0|syslog|info|rsyslogd-2359|action 'action-7-builtin:omfwd' resumed (module 'builtin:omfwd') [v8.2402.0 try https://www.rsyslog.com/e/2359 ]
2024-04-18T17:14:52.313768+00:00 5698cff1480e rsyslogd CEF:0|syslog|info|rsyslogd:|[origin software="rsyslogd" swVersion="8.2112.0" x-pid="1" x-info="https://www.rsyslog.com"] exiting on signal 15.
2024-04-18T17:14:53.000492+00:00 5698cff1480e rsyslogd-2442 CEF:0|syslog|warning|rsyslogd-2442:|environment variable TZ is not set, auto correcting this to TZ=UTC [v8.2112.0 try https://www.rsyslog.com/e/2442 ]
2024-04-18T17:14:53.000895+00:00 5698cff1480e rsyslogd-3000 CEF:0|syslog|err|rsyslogd-3000:|unknown priority name "" [v8.2112.0]
2024-04-18T17:14:53.001913+00:00 5698cff1480e rsyslogd CEF:0|syslog|info|rsyslogd:|[origin software="rsyslogd" swVersion="8.2112.0" x-pid="1" x-info="https://www.rsyslog.com"] start
2024-04-18T17:15:22.558959+00:00 5698cff1480e rsyslogd CEF:0|syslog|err|rsyslogd:|Malicious PTR record (message accepted, but used IP instead of PTR name: IP = "172.27.0.1" HOST = "172.27.0.1" [v8.2112.0]
2024-04-18T22:59:52.551745+05:45 blink kernel CEF:0|kern|info|kernel| vethd47ebd2 (unregistering): left allmulticast mode
2024-04-18T22:59:52.552037+05:45 blink rsyslogd-2027 CEF:0|syslog|err|rsyslogd-2027|omfwd: remote server at localhost:20514 seems to have closed connection. This often happens when the remote peer (or an interim system like a load balancer or firewall) shuts down or aborts a connection. Rsyslog will re-open the connection if configured to do so (we saw a generic IO Error, which usually goes along with that behaviour). [v8.2402.0 try https://www.rsyslog.com/e/2027 ]
2024-04-18T22:59:52.552118+05:45 blink rsyslogd-2007 CEF:0|syslog|warning|rsyslogd-2007|action 'action-7-builtin:omfwd' suspended (module 'builtin:omfwd'), retry 0. There should be messages before this one giving the reason for suspension. [v8.2402.0 try https://www.rsyslog.com/e/2007 ]
2024-04-18T22:59:52.552413+05:45 blink rsyslogd-2027 CEF:0|syslog|err|rsyslogd-2027|cannot connect to localhost:20514: Connection refused [v8.2402.0 try https://www.rsyslog.com/e/2027 ]
2024-04-18T22:59:52.647657+05:45 blink kernel CEF:0|kern|info|kernel| br-ce2e2d75e3ae: port 1(veth9ea461f) entered disabled state
2024-04-18T22:59:52.947675+05:45 blink kernel CEF:0|kern|info|kernel| eth0: renamed from vethbf2d96a
2024-04-18T23:00:22.556242+05:45 blink rsyslogd-2359 CEF:0|syslog|info|rsyslogd-2359|action 'action-7-builtin:omfwd' resumed (module 'builtin:omfwd') [v8.2402.0 try https://www.rsyslog.com/e/2359 ]
```
### Test the custom log from your host machine or otherside
```bash
echo -n "<14> Test TCP syslog message" | nc -w1 localhost 20514

```
### Check the line in reciever container for log reception in CEF format
```bash
root@491613d1811e:/# tail -f /var/log/syslog.cef.log
```
#### Output:
```bash
2024-04-18T17:15:53.603302+00:00 172.27.0.1 - CEF:0|user|info|| Test TCP syslog message
2024-04-18T17:16:14.114755+00:00 172.27.0.1 - CEF:0|user|info|| Test TCP syslog message
2024-04-18T17:16:43.565195+00:00 172.27.0.1 - CEF:0|user|info|| Test TCP syslog message
2024-04-18T17:17:29.051571+00:00 172.27.0.1 - CEF:0|user|info|| Test TCP syslog message
2024-04-18T17:18:47.172841+00:00 172.27.0.1 - CEF:0|user|info|| Test TCP syslog message
2024-04-18T17:18:54.057606+00:00 172.27.0.1 - CEF:0|user|info|| Test TCP syslog message
2024-04-18T17:19:00.170437+00:00 172.27.0.1 - CEF:0|user|info|| Test TCP syslog message
```

## You can send from other log source to relay container on port 20514
## Enjoy !!!!!
