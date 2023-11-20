# pedestal-play

## Getting Started

1. Start the application: `lein run`
2. Go to [localhost:8080](http://localhost:8080/) to see: `Hello World!`
3. Read your app's source code at src/pedestal_play/service.clj. Explore the docs of functions
   that define routes and responses.
4. Run your app's tests with `lein test`. Read the tests at test/pedestal_play/service_test.clj.
5. Learn more! See the [Links section below](#links).

## API Documentation

| Endpoint     | HTTP Method | Description                                    | Interceptors                |
| ------------ | ----------- | ---------------------------------------------- | --------------------------- |
| `/`          | GET         | Returns the main page of the application.      | `home-page`                 |
| `/about`     | GET         | Returns information about the application.     | `about-page`                |
| `/debug/:id` | POST        | Activates the debugging page for the given ID. | `debug-page`                |
| `/hello`     | GET         | Returns a greeting message.                    | `msg-play` and `hello-page` |
| `/events`    | GET         | Initiates an event stream using SSE.           |                             |

## Test WebSocket in REPL

### Postman

```sh
ws://localhost:8080/chat
```

### Run project

```clojure
lein repl
(def srv (run-dev))
(pedestal-play.service/send-message-to-all! "Hello from Pedestal Server!")
(pedestal-play.service/send-and-close! "Goodbye from pedestal server!")

```

[Postman Documentation API's](https://documenter.getpostman.com/view/30581720/2s9Ye8gFX5).
[Postman Documentation WS](https://documenter.getpostman.com/view/30581720/2s9Ye8gFX5).

## Configuration

To configure logging see config/logback.xml. By default, the app logs to stdout and logs/.
To learn more about configuring Logback, read its [documentation](http://logback.qos.ch/documentation.html).

## Developing your service

1. Start a new REPL: `lein repl`
2. Start your service in dev-mode: `(def dev-serv (run-dev))`
3. Connect your editor to the running REPL session.
   Re-evaluated code will be seen immediately in the service.

### [Docker](https://www.docker.com/) container support

1. Configure your service to accept incoming connections (edit service.clj and add ::http/host "0.0.0.0" )
2. Build an uberjar of your service: `lein uberjar`
3. Build a Docker image: `sudo docker build -t pedestal-play .`
4. Run your Docker image: `docker run -p 8080:8080 pedestal-play`

### [OSv](http://osv.io/) unikernel support with [Capstan](http://osv.io/capstan/)

1. Build and run your image: `capstan run -f "8080:8080"`

Once the image it built, it's cached. To delete the image and build a new one:

1. `capstan rmi pedestal-play; capstan build`
