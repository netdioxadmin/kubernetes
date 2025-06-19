# Kubernetes Data at rest encryption
## For Encryption we need to generate a 32 bit key and should be also encoded in base64. 
```
openssl rand -base64 32
```
### Output will be similar
```
openssl rand -base64 32
y1+lm/6qxExUb7G+csUc+OTq3/BRBeZ2Xw5Eg/NGwnw=
```