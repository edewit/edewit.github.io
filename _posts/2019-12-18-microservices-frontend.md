---
layout: post
title: Microservices Frontends
date: '2019-12-18'
tags:
- micro-services
author: Erik Jan de Wit
---
*UPDATE 5 Apr*
added link to the [source of the "stitching layer" layer][3] and it contains links to the other services

The microservices mentioned in my [previous post][1] use the vertx event bus to communicate with each other.
An event bus is of course a great way to separate services and have them coupled loosely.
I've used the same technique for the webcomponents the carousel emits an event for the current photo that is being displayed.

```js
  this.$emit("photoId", this.photos[this.counter].id);
```

A great addition to this project would be to use the vertx client side event bus to listen to the server events and update the state of the components.
That way, when different clients "perform a like" for a specific photo, our view will automatically reflect that.

As mentioned on the [previous post][1] I created a "stitching layer" app that uses react.
Optimally we wouldn't have to do this so we have no coupling at all, in it's simplest form we still would have a index.html that includes all the js code of the services.
But this is an easy first step that works.

This is what the app now looks like, the components marked in red are from the photo service, blue is the like service and finally green is the query service.

![stitching layer ui](https://lh3.googleusercontent.com/n4qaF71RykQgxXPPYWTsA-9nM9FFb3unaXgKnkCV1_pbnI_HwMjZMKOyqjz_Rk2QAs6iXdninuvESJgvsJW5WFS4hNLleTGHdXLvk10wD0iNGLUQq5_NERAWFCnWwsgf_kBvN86NVY9w_VOz8-0kYHLryhLmg8kB2LWipU5qEuS7KoawbZh97iZjQFlL2EUAVe784iNoRk3AoK2wIOD1Y_ocZDj4_SjjZHgWPF2c58x7OltGgRfUiGGqBf_uYdzRwSxcpzHinkNdwKLsYMPsaz7sqP6J0LiNXkegJ7Cec9x5fnoaqNsqDwQtPcsCQloqz2cyCi6oN2UWGXDnfXqnPvzjBHm8HVTeY1WC5ll1JVCRUi_FKuAEqYSZ0oJ8tpQMaSCmPrVb5rIhiyZguJApKnUjHHvwbqUyF8fQo0istWGpXv4VvZG01THizbqlW-GlOT4LDHmpHvOLn6U9iy-P50grWb1NQ1u_KnN10CXLvyc6OVi831hebi2qK0onNumnszb8hlxJ1o7F1I2Z1FsNx-5HLW1ddVInridpZX_6EbqaHyxaJq9IMZCZ2SMgtsdSpvhAm5AEL_RUD3k8zQ0jV9G8V0Oc1dLajJ6HVP_CQa60GpWVZ9p75VvHK85ROx3nknMViewXdxxj9-y1PeU_edv38nydiwDEKGNkiYQwmNbXnlJ3l_5KDjdGr1ABs25jdd9T4zNTYJmxTy7V_ZVNE-QbVZCijsjtX16xlHpglkRXjf8=w1384-h698-no)

A diagram from what we now have the "stitching layer" is still coupling:
![stitching layer](https://lh3.googleusercontent.com/IlvYJ8OsYGdWz9rw_tBeXz7llcpNPjmVlt2_wKNjpFJafeSRQLOpy6-KHiB99hTtSQsMMBzv607Mbjt8krC_JelrC84wqkw7lfHZz19hHVTHCZAmBGCgy1OOExednujpF8jpIFldCNvJUi6vvtFVnYvW1v7-7bK4BjLmYDDEQSkrf8yXcMxtbuQeutNWUynSCnfRhg1H08vhQuVK0Y2miBX82yL53ZCgzhknvb2jk9sSzPbGeNIc6FSRrqIF2R_5J55tpt5imU9L1OxV5iqmUPwa9baVQ0nXOha6lWmlwfzB9OszkV4JHwEZnGxV-udK8cVS2y7aW9KZnhPygTH21eCCOGTMgE2ETrdMFUpqRjKW7KuQ_RVX3CUWUw220AUfkgiR6BDO_hwcUa0304d3FTR_zLLdnTqKVg7lTTvmV_KQIbwXPRmRlAjGue6eYajbi8viReOqiMxH4sDwKbJrngBKlkXOHoGltDxUMxkurXf8mwjYaMpIH4UhbNYNTw2u7a3kuRZoLYAiXT1qpahNRPyeFIzf51DkCrm5AqdvV9dSPPMBas5BQfOGbvDH7hCRlcLTXgC4KbFzjJpbvP_99Xsc8Wzz2RWbu3jWh2N-f-GGWuQtPnXpaug-c1xUFk18-6ELPGEPfzzq6MNRBYDW60XUQ6VR87UMiYy6zdl8MIf4GGH-YHc1nDdE3TInLuBRyv4iE0YrW_Hz3GD0t9EEfWKHuzs_tjHZ8vOF91Y-v5M9tx0=w361-h371-no)

There is also a transparent proxy to make our request go to the right microservice:
![proxy](https://lh3.googleusercontent.com/3P4IaFMKecfeGqiLfH4AuYfnpI4hqQO6PnhYRmh35XWf7gv4ySxiAM67Zk0u0TmhAcdbduVKZPGU5ZsOPAAJKyOvqYv7s5TWj1azV-jIuegxXniCsb_yKq60Szsebp_qOevRNeBzez3zHo84ujUxUyZuvu_j7hZ7n0sUoTo28ymvsm2BknxUEWlTKMegHfbffTqsvkMqlVksK6-6bxWu_ErI9UJzsFcMFoFvK51yJtMH9gorIlGFFk_K5ZqXo0eWcRnW8MdPvcGzPW9HgoTeouJJI5SGVLOjcrpmcVexUTUzjygSBMlaXyRWkfs7r7VPgiGpyw7iOQGoHa9_cFsQ_B8vggXP-slerQTFdV9c9lkrxbzq0LfRzjwR-49ctyY4G7obVWcFP_CVpxsBfW7jXOcqtDPEgJzdcR912BWnEiiFpvgnKLcl0En5hAVftD0Yj0CP6x7Ubo41T2O8bWCFXuXeSg08fubyLkqgargn_VqzDSHcU9hF4WiguHppFM1lZFc_FiOS79N3oS6PZE4W3vxqnXqrEAQtUPBhW_UORlRVILJGYXYkkB4oZyNs6n-qZp_Pu5qMWR65zgAB7Gx_dWAmnFD7jiYXBUpNAKxdf1qezrtvtzOe-dxKf0aVnfeemYh3-9AcdYx55NCKe1Rm4a4NqUwQPUkTP6vcmNqOXKUhaO7lj11nXAhCJhLR3bmk-Qe3AR5u9k32TPvW3h_twy3gzL1Pj6HG60MMSs-55tic1sw=w449-h301-no)

In production we'll have to setup this routing some other / better way.

Second challenge that I bumped into was styling.
When you use webcomponents they use the shadow dom and css styling is local.
The way I fixed that now is by using css variables defined in the webcomponents and then set or overridden in the "stitching layer".
But for a production ready type application you would probably want to make your own [patternfly][2] type project or have some sort of style guide.
Downside of that is that your introducing more coupling, another way is to have shared css vars, but then you are duplicating components.

Next and final thing that we need to think about is server side rendering.
Obviously this is something that we would like to have when we have so may different smaller parts and possible different frameworks.
Server side rendering could potentially also remove the need for a "stitching layer" and when done really well help us with developing these kinds of microservices apps.

One of the conclusions that we can make at this point is, although theoretically we could build all of these frontends in any framework, in practice we would want to minimize the number, as it will increase the size of the initial download.
At a minimum we would have to use the same version of the frameworks.

The [source of the "stitching layer" layer][3] and it contains links to the other services

[1]: /2019/12/16/microservices-frontend.html
[2]: https://www.patternfly.org/v4/
[3]: https://github.com/edewit/photo-frontend-common
