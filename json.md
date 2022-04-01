Installing `jq` in Linux

```
yum install epel-release -y
yum update -y
yum install jq -y
jq --version
```

If it doesn't work and it asks you to have a `root` property, 
```
sudo -i
```

If it doesn't work,

wget https://github.com/stedolan/jq/releases/download/jq-1.5/jq-linux64 -O jq
chmod +x jq
mv jq /usr/local/bin
```

To get the top level keys

```
jq 'keys' file.json
```

To get the entire json from the website 
```
curl -s www.example.com | jq .
```

To get the value of a certain key
```
curl -s www.example.com | jq .key 
```
