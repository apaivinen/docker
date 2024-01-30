# Powershell container
keep your local powershell session clean!

contains following files:
- Dockerfile

Build command

```powershell
docker build -t apa/powershell:latest .
docker build -t powershell .
```

Run command
```powershell
#--name imageName
#--rm Automatically remove the container when it exits
#--interractive takes you automatically to the container when it starts
docker run --rm --interactive apa/powershell:latest
docker run -v D:\\docker\\scripts:/scripts --rm -it powershell:latest
```

Configure terminal Tab. DOES NOT WORK YET

```json
{
  "opacity" : 0.95,
  "closeOnExit" : true,
  "colorScheme" : "Campbell",
  "commandline" : "docker run --rm --interactive apa/powershell:latest",
  "cursorColor" : "#FFFFFF",
  "cursorShape" : "bar",
  "guid" : "{c5527a4c-fd03-4f40-8f30-5067cb7cf201}",
  "historySize" : 9001,
  "icon" : "ms-appx:///ProfileIcons/{9acb9455-ca41-5af7-950f-6bca1bc9722f}.png",
  "name" : "Docker powershell",
  "padding" : "0, 0, 0, 0",
  "snapOnInput" : true,
  "useAcrylic" : true
}
```