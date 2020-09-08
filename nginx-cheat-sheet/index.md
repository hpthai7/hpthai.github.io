# 

Study the impact of trailing slash in nginx/ingress configuration

Imagine a hello-world service that provides a static website with / returns the homepage, and the homepage references to different children pages by using `href=/hello-world.html`.

```html
Hello World. Reference to <a href="/hello-world.html">an URL</a>
```

This page is stored in an nginx container.
The basic micro-service should return results for the following requests:

https://www.sample-page.com/
https://www.sample-page.com/index.html


The ingress configuration that distributes requests to the microservice via the path /hello-world:

https://www.sample-app.com/hello-world
https://www.sample-app.com/hello-world/
https://www.sample-app.com/hello-world/index.html



