# syslog-CEF-relay
syslog formated log to CEF (RFC5424). It will conver the syslog default syslog formatted log to CEF (RFC 5424) log. 

# Instruaction and Information
|    S.N     | Container Name     | Purpose                |   Port     |  Protocol |
|----------- |--------------------|------------------------|------------|-----------|
| 1          |  relay             |   To convert default   |  20514     |  UDP/TCP  |
|            |                    |   syslog data to CEF   |            |           |
|------------|--------------------|------------------------|------------|-----------|
| 2          |   reciever         |   Enpoint where CEF    |  30514     |  UDP/TCP  |
|            |                    |   log format is needed |            |           |
