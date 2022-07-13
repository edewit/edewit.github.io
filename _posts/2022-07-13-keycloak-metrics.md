---
layout: post
title: Keycloak metrics
date: '2022-09-13'
tags:
- keycloak
author: Erik Jan de Wit
---

In the new design of the admin ui of keycloak we wanted to include a dashboard with some statitics, why, because dashboards are cool and they look nice 😊
![Design](https://marvel-live.freetls.fastly.net/serve/2021/1/02af6b8ee3c54262a3c17ce94e3a5531.png?quality=95&fake=.png)
We could add even more gauges and graphs of course, but why not use something that is already there like [Prometeus][1] and [Grafana][2].

[Aerogear][3] has a SPI that exposes a Pormetheus `/metrics` endpoint and a Grafana dashboard to go with it so let's install that:

```bash
cd /tmp
wget https://github.com/aerogear/keycloak-metrics-spi/releases/download/2.5.3/keycloak-metrics-spi-2.5.3.jar
```

to install it copy it into keycloak I'm using the quarkus based version:

```bash
cp /tmp/keycloak-metrics-spi-2.5.3.jar /opt/keycloak/providers/
```
restart keycloak and enable the `metrics-listener` in the admin ui: "Realm settings" -> "Events", select `metrics-listener` from the dropdown

![Enable metrics listener](https://lh3.googleusercontent.com/NWUuyXJT9xLVu2BKLzJAsvqfM_yand0XfyuJYHp1xKc5BSidu_OC8Ffdp1I8pscCZ80VzM3MSpKmArzwg6iQuIxH_1Ti4of2EVDN22iV7L4hjZKneJ5deDPPfpVAZtzJhOnT8U80zHcsEkQPohqQbZtJocKYS_e2pqWjmYXpkJlR-ZPCR1R80dka-y32CHbG351WbDqI0pLj8LQyfjQqX4VtRfKDyHFK9UMWKAwRBSTuIy0NgbEjExDwOUoCmOWq6QXqUS2BH-jsNhv5w484SD1rA0GgB4ot59civBAa1Cqa-y0aMP7d-Sog1eLnDkCNGGT4AEOAzAGiiKmSTlPX5WyyjDC7r-NvG_wI9Il4ZAjL45oJTM9734LYf_m3aft5hy4VfBz3x0EjFAYsgAi2so8GqhN8Wu-5kqaWq95KE-oFHOgjx_opKAsEPlvhq9mtjYKUb0LcEKNUVkHkhro4NdXcYJ49B1IvDZUaJicDn9iXoPiZ08WRdyOyK_7cFMSTgg_IHOh22lKDHV4ZbjD8dMnVxTcppxXKq1v3ZclYGwPo0KpaXijcy2WbKhly6s5As_Osvida8po1OFVBP9baWH8oP3F2PvU2rD0w2qL3WHAu8OvHY8O7f3eOtqari2R9OWYX8VWCFiMAOZLnduHjdL_0XRrgwIpuuprkmuOKcIB-h4sm8b51XXr6EGdfn4jzPQg6zbyKWthLcAFYcR9eai5V0_0QJVcYnNOtG2Zmx7Xi8kciRmaVemg2204JzA3jZ5600LFMKi6h_X_2Zl-SwrnIPNIA3SVymJTWd37lSM2Nbp6kQ_At45PnDI7O2nugJDm2yQ2X03z69zrTfhaGJN58BRk=w921-h505-no?authuser=0)

All we have to do now is install Prometeus and tell it to consume this endpoint

```bash
curl -LO https://github.com/prometheus/prometheus/releases/download/v2.19.1/prometheus-2.19.1.linux-amd64.tar.gz
tar xvf prometheus-2.19.1.linux-amd64.tar.gz
cd prometheus-2.19.1.linux-amd64
```
Then edit the `prometheus.yml` to add the keycloak endpoint

```diff
23c23,24
<   - job_name: 'Prometheus'
---
>   - job_name: 'keycloak'
>     metrics_path: '/realms/master/metrics'
29c30
<     - targets: ['localhost:9090']
---
>     - targets: ['localhost:8080']
```
[see the whole file][4] and start it with `./prometheus`

Install grafana and set it to use Prometheus as the data source:

```bash
wget https://dl.grafana.com/oss/release/grafana-9.0.2.linux-amd64.tar.gz
tar -zxvf grafana-9.0.2.linux-amd64.tar.gz
cd grafana-9.0.2
./bin/grafana-server
```
open `http://localhost:3000/` and login with `admin` and `admin` set Prometheus as data source `http://localhost:9090`

![Set data source](https://lh3.googleusercontent.com/25bnsBkCQJ9z-5ceYM-zJD2_SRH9-MZjwep8M0sdaaHqhKDoFh-K9x4dTFKsYKHlBdTeekYjaXUIK4adXPRgWvwArB5p1BTIBQuqXmH1UP1VMK8ITcwsHQ6L0garp2Z5In87BFX5QoAPNCjtmLLoK7o7J3fDkKz156n3nBgRbP8PCAkKTER9TfY1JL3-0lquxE60G-mlWDqJSGW1bvtblCg1gNiOQwT3-JrP04U2woa6r3_XTjxDnVLPV8QTQzirEHSIvcPuyqzT-ohEEiD6W_pyav3y0LSZr5KKNnEvjTKyxl1ZlmElg7Q13wWbdn4DBgg-Am4sost58jWMcOLvV6KiPHsyKjVWQwSk8VaEz5jqzLp11NwP0-6Nd-oF92I18SIFTz7Xkbh5SpqJuYNwyxS0PuJqavyjFTGxoCOYA5s-UOsS9Fq696lLkzcvVeQ5OuC77tAoRrDttPeGva0lvKooN9Hn1TeticgGAVTgS-YzNjwncT81o_4af_uER6o9u6F7b6ThUObJBJHiOx_o8KS5cz5jr7l3vxWQoPyqeu2d49ONJL5riwkvflbQwh0shDnjtSKzlgwmeKC6bXZezJWHDCG-uEzkOjfcfEMQOE4_F92T09ORijmA1I75lES91JareNdHeliCBcS82MAtAPrXCtRTALX3lBpeqBTx3Z1gxbhIGWkyDPYYl86BMv59UnkacrWbTnr9SkDgFkA7_QWCZmxclMf7EWxoUgX-iEPMP75PlQ5-ERp_f9eI98u29tSVwHGeLAojcAd_e4x9EAL-QloapK7JOiEHVyt83LrC7BaQmPzcmLR_TTJQpIl8wFRvdEH9C3zr4Gs5Da-ugwYgkx0=w1407-h544-no?authuser=0)

then import the dashboard of the aerogear/keycloak-metrics-spi "Dashboard" -> "Browse" -> "Import" and enter the id: `10441`

And there we have it this beautiful dashboard:

![Grafana keycloak dashboard](https://lh3.googleusercontent.com/caPHTnN2G4A-ceIjBVktt_7n00ADdojaWZvWJtgVOqLHd0kcGNjxP7nBglba4DkE4ZYzgye0uV3plEOhYIVjVH9bUWVc6QNmIRDP1Pnc1ZjAZag6reVYQCm-ROTHvJHSilT-v6WDbZxiirq-rOupwwgqzBoLvbWvha8yvLDyqgpdrUOsXWEZGsr6ANrpE4bXazgtoTzfCQTJSsMzls-VuzAQwIi20dyoMApI-jc2v48fPeRCGElxOvlg1DGnY_ZhLgpdp-BheRbgYaB69gua2_d35UqTBLaS_DVuPW5SDknFznMZpjsXOuzN5UF7XfGXZIYK_cZr1lZ_LX0Vkl1lQ8hQr-HCDAEkZ-KMtCXlVMhckgohlO_dGvklDUi_Fr-SEiMHiEZl57oxNdarCx2jLXR_ehUkj-qVyBNoplN___iR1Bs9sdCvXDuZca94mH0MAkhxwRo4WsVfEE3IFYfYPjYRlH7ciJ9sQVNus7eME6FarzK5DUI-2jO8NNRtsCHweUDtduqmJTQK6En9wq6EJlUVCciEJ6g6-EK-eey4srbQQmlp3hlFcPwdHTFOC1PlAbPoyViDBO6LcjAaDoPJhuTqJddnlJOfMyu5d2ja-JKcg0TJzV6y6ydAiKjqDSnVqGaZ2-F3L-DiY3F96ebImPnkuNZf3oWjifSkBHsX4RohyDEVxBF3NnkZGUF9aDhcGQmI8ddHUf4IQ7ZL8q0d3H3818CF2Ye0mcdXI7C5qBVwQFJoXyusoPGMnzVzmRJtZKsql96SrIluvyaqXZ-OW04hxLQqFIfC99IFWYt5IaYHf_QnTKmSFnawNv1y0lNl8fJwQ_CdXCEwi1TPgAUE9gXd_OU=w1208-h783-no?authuser=0)

[1]: https://prometheus.io
[2]: https://grafana.com/
[3]: https://github.com/aerogear/keycloak-metrics-spi/
[4]: https://gist.github.com/edewit/0a270edc6ff43c6cfb5300a1ac857009
