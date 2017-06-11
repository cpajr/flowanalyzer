# Searching in Kibana
The syntax used for searching in Kibana is based on the [Apache Lucene syntax](http://lucene.apache.org/core/3_5_0/queryparsersyntax.html). There are a few "gotchas" to bear in mind, but once you get the syntax down it's not hard. Spaces in field names MUST be escaped by a "\" symbol. Binary operators like "AND", "OR", and "NOT" MUST be all UPPERCASE. You can search for individual fields and terms, or combine them. Multiple statements can also be combined by putting them in parenthesis. 

Check out the [official Kibana documentation](https://www.elastic.co/guide/en/beats/packetbeat/current/kibana-queries-filters.html) for more information, and test out the examples below.

Search for a keyword ("SSH") in _any_ field:
```
SSH
```

Search for the keyword "TCP" in the "Protocol" field:
```
Protocol: TCP
```

Search for the Transport-type protocol numbers in the "Protocol" field:
```
Protocol:[6, 17, 33, 132]
```

Search for 3389 as a Source or Destination port number:
```
Source\ Port: 3389 OR Destination\ Port: 3389
```

Search for 3389 or 3390 in the Source or Destination port number:
```
Source\ Port: (3389 3390) OR Destination\ Port: (3389 3390)
```

# Searching by Protocol
Search by either protocol name ("TCP", "UDP", "OSPF", etc) or [IANA protocol number](http://www.iana.org/assignments/protocol-numbers/protocol-numbers.xhtml).

## TCP
```
Protocol: TCP

Protocol\ Number: 6
```

## UDP
```
Protocol: UDP

Protocol\ Number: 17
```

## Transport Protocols
```
Protocol: (TCP UDP DCCP SCTP)

Protocol\ Number: (6 17 33 132)
```

## OSPF
```
Protocol: OSPF

Protocol\ Number: 89
```

# Searching for Traffic Profiles
Combine search terms to search for traffic profiles. Different methods of searching for traffic profiles are shown.

## Web Traffic
```
Protocol\ Number:6 AND (Destination\ Port: (80 443 8080) OR Source\ Port: (80 443 8080))
Traffic\ Category: Web
```

Search for individual types of Web traffic:
```
Traffic: HTTP
Traffic: HTTPS
```

## SSH Traffic
```
Protocol\ Number:6 AND (Destination\ Port: 22 OR Source\ Port: 22)

Traffic: SSH
```

## DNS Traffic
```
Protocol:[TCP, UDP] AND (Source\ Port:53 OR Destination\ Port:53)

Traffic: DNS
```

## Microsoft RDP Traffic
```
Source\ Port: (3389 3390) OR Destination\ Port: (3389 3390)
```

## VNC
```
Source\ Port: 5900 OR Destination\ Port: 5900
```

# ---
**Copyright (c) 2017, Manito Networks, LLC**
**All rights reserved.**