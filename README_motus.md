### SSH server for networked sensorgnome receivers ###

This is a fork of openssh's sshd which supports a new option for keys
in the authorized_keys file: `single_remote_forwarding_port=N`, which
means the client connecting using that key can only map a single
remote (i.e. server) port, namely the one specified as `N`.  This is
used to give each sensorgnome a unique tunnel port (in the range
40000...65535 ).  When the SG connects to the server, it will map the
tunnel port on the server back to its own ssh server on port 22.  This
lets us ssh into the SG, without requiring that the SG's ssh server
listen on any external network interfaces, and without any firewall
openings required on the SG's network.  (The SG must of course be
able to reach our server with an outgoing ssh connection to
port 59022 on sensorgnome.org  or sgdata.motus.org )

e.g. The Old Cut sensorgnome SG-5113BBBK2972 as tunnel port 40407.
When connected to the server, it can be reached from the server
by doing:

```
ssh -p 40407 bone@localhost

```

(and then entering the password `bone`).
