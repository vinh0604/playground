## Iteration 3

As you know, the previous app was entirely self-contained. In the real-world, most apps are depending on some sort of service, e.g. database, search-server or a key-value store. Let's use Redis to provide our app a dynamic backend.

### Preparation

Checkout the code for the third iteration.

```
cd /vagrant
git checkout iteration-3
```

### Redis

The Docker repository name is ```dockerfile/redis```. Go ahead and start an instance and expose its port properly. You should start it daemonized with the flag ```-d```

Note: The redis default port is ```6379```

You can easily check if it's running and the port is exposed by trying to connect with the redis-cli.

When it works, it looks similar to this:

```
redis-cli
127.0.0.1:6379>
```
### App

As we've got new code, we have to rebuild the Docker container. Thanks to the Dockerfile, that's pretty straightforward.

```
docker build -t playground/smartypants:<YOUR-NAME> .
```

The app is preconfigured to talk to a redis server on ```192.168.33.10```, so as long as you've expsoed the right port it should work.

Let's try

```
docker run -p 9292:9292 playground/smartypants:skorfmann /bin/bash -c "bundle exec rackup config.ru"
```

And visit [the app](http://192.168.33.10:9292/)

#### Hook it up

Ok, now that we have a redis container running, let's hook it up with our app server. All containers are connected via the ```docker0``` networking bridge and can talk to each other.

So, we know the port already (6379), now find out the ip address of the redis container.

When we're going to start the app container, we'll provide REDIS_IP and REDIS_PORT as environment variables.

 
### Volumes

```
docker run -d -p 6379:6379 -v /home/vagrant/redis:/root dockerfile/redis
```

### Dynamic Linking

