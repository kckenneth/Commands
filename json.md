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
