# Rails Nginx Unicorn
Easily configure docker for Rails production with Nginx and Unicorn.

## Included
- Nodejs
- Nginx
- Unicorn
- Foreman

## Usage

### 1. Setup Dockerfile

Create a `Dockerfile` at the root of your project and paste the code below. You may make changes as required

```
# Dockerfile
FROM ishouvik/rails-nginx-unicorn:latest
MAINTAINER Your name <yourname@example.com>

# Set workdir
WORKDIR /app
COPY . /app

#(required) Install Rails App
RUN bundle install --without development test
```

### 2. Build docker image

```
# Build image
$ docker build --tag yourproject .
```

### 3. Run Docker container on the newly created image

#### 3.1. Using Docker terminal command

```
# Run container
$ docker run -d -p 80:80 -e SECRET_KEY_BASE=yoursecretkey --name yourproject-1
```

#### 3.2. Using Docker compose

  - Create a `docker-compose.yml` file at the root of your project and paste the following code

  ```
  # docker-compose.yml
  version: '2'
  services:
    web:
      build: .
      ports:
      - "80:80"
      env_file:
        - ./production.env
  ```

  - Create a `production.env` file at the root of your project and paste all your environment variables such as your `SECRET_KEY_BASE`, database password, etc.

  ```
  # production.env
  SECRET_KEY_BASE=yoursecretkey
  ```

  - Run `$ docker-compose run`
  > Please note: This is a very basic `docker-compose` setup. You can find more information about docker-compose [here](https://docs.docker.com/compose/overview/).

