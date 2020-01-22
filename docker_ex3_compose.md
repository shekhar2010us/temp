## Manage multiple containers with docker-compose


#### Install docker-compose

```bash
sudo curl -L https://github.com/docker/compose/releases/download/1.22.0/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose

sudo chmod +x /usr/local/bin/docker-compose

docker-compose version
```


We will build a simple Python web application running on Docker Compose. The application uses the Flask framework and maintains a hit counter in Redis. While the sample uses Python, the concepts demonstrated here should be understandable even if you’re not familiar with it.



### Steps


Start by creating a directory called ```composetest``` where we'll create the following files:

```shell
mkdir -p /home/ubuntu/code/composetest
cd /home/ubuntu/code/composetest
```

- [app.py](#apppy)
- [requirements.txt](#requirementstxt)
- [Dockerfile](#dockerfile)
- [docker-compose.yml](#docker-compose.yml)


#### app.py

Create the **app.py** with the following content:

```python
import time

import redis
from flask import Flask

app = Flask(__name__)
cache = redis.Redis(host='redis', port=6379)


def get_hit_count():
    retries = 5
    while True:
        try:
            return cache.incr('hits')
        except redis.exceptions.ConnectionError as exc:
            if retries == 0:
                raise exc
            retries -= 1
            time.sleep(0.5)


@app.route('/')
def hello():
    count = get_hit_count()
    return 'Hello World! I have been seen {} times.\n'.format(count)
```

#### requirements.txt

In order to install the Python modules required for our app, we need to create a file called **requirements.txt** and add the following line to that file:

```
flask
redis
```


#### Dockerfile

Create the **Dockerfile** with the following content:

  ```docker
FROM python:3.7-alpine

WORKDIR /code

ENV FLASK_APP app.py

ENV FLASK_RUN_HOST 0.0.0.0

RUN apk add --no-cache gcc musl-dev linux-headers

COPY requirements.txt requirements.txt

RUN pip install -r requirements.txt

COPY . .

CMD ["flask", "run"]
```

#### docker-compose.yml

```docker
version: '3'
services:
  web:
    build: .
    ports:
      - "5000:5000"
  redis:
    image: "redis:alpine"
```


### Build the image

```bash
NOT REQUIRED
THIS WILL BE DONE IN COMPOSE ITSELF
```

### Start the compose


```bash
sudo docker-compose up
```


Head over to `http://<aws_public_ip>:5000` and your app should be live.

