# karmabot
Slack bot for trolling karma. 

## What? Why?
In a slack channel I use there is a bot which has a karma module.  Messaging the bot with "fubar++" or "fubar--" will add or subtract the karma value for fubar. This was created as a troll response to a "war" of sorts between perl and ruby developers in slack.

This docker image runs a ruby script to add positive karma to ruby and negitive karma to perl with a random sleep between 5 and 15 minutes.

## Running in Docker
```bash
docker pull busybox42/karmabot
docker run -it --restart=always --name karmabot -d -e TOKEN=<Legacy Slack Token> -e CHANNEL=<channel id> busybox42/karmabot
```

## Building Manually
```bash
git clone https://github.com/busybox42/karmabot.git 
cd  karmabot
docker build -t karmabot .
```  
  
## Running with Kubernetes
Because who doesn't want to scale their trolling?

To run in kubernetes first manually build the image.

After the image is built you can either run this command:

```bash
kubectl run --image=karmabot karma-app --env="TOKEN=<Slack legacy token>" --env="CHANNEL=<channel id>" --image-pull-policy=Never --replicas=2
```

or modify the karma-app.yaml file adding your legacy token and channel id:

```bash
kubectl apply -f karma-app.yaml
```
