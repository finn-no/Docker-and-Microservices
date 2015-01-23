# <br/>Docker and Microservices
## A match made in heaven!?
<br/>
<br/>
#### **Stig Kleppe-Jørgensen**
FINN reise

Note:
Nå tenkte jeg jeg skulle vise dere hvordan Docker løser alle utfordringene vi har rundt microservices, for den gjør jo det, ikke sant?? Hmm...la oss se litt nærmere på det.

----

# Build

Note:
Først så pakker vi tjenesten i en container

*"Finally a universal package format!"*
Bedre enn rpm/deb eller jar/war, dvs ikke system- eller språk-spesifikt

----

# Ship

Note:
Deretter flytter vi containeren til de maskinene den skal kjøre på
Og husk, dette blir akkurat den samme koden/konfigurasjonen overalt

----

# Run

Note:
Til slutt kjører vi containeren, dvs. tjenesten vår

----

# Any application

Note:
Enhver tjeneste kan kjøre i en container.
Vel, alt som kan kjøres på Linux, i hvertfall. Det er riktignok planer om å supportere andre platformer, som Solaris (zones) og BSD (jails)

----

# Anywhere

Note:
Og den kan kjøres overalt:
Lokal VM, skyen, rett på jernet, etc.

----

## Aren't you forgetting something?

Note:
Men dette dekker jo ikke alle utfordringene en har med microservices

----

<!-- .slide: data-background="img/microservices_word_cloud.png" data-background-size="100%" -->

Note:
Her er en liten tag cloud på utfordringer rundt microservices<br/>
Mange av utfordringene går på eksploderingen av antall tjenester.
Docker vil ikke svare på så mange av disse utfordringene alene, men ved at Docker har gjort containere populære og lette å bruke, har det kommet til masse verktøy for å støtte opp om disse.

----

<!-- .slide: data-background="img/lego_falcon.jpg" data-background-size="100%" -->

Note:
Og dette er ikke bare et tilfeldig bilde...

----

> If a Docker application is a Lego brick, Kubernetes would be like a kit for building the Millenium Falcon, while the Mesos cluster would be like a whole Star Wars universe made of Legos

Note:
Kubernetes og Mesos er altså verktøy for å kjøre Docker containere

----

# The Datacenter Operating System

Note:
Mesos kaller seg dette (driver hele infrastrukturen til Twitter bl.a.)

----

# Accelerate Dev and Simplify Ops

Note:
Mens dette er taglinen til Kubernetes fra Google<br/>

Mesos, et Apache-prosjekt, og Kubernetes fra Google blir gitt et cluster med maskiner og styrer så hvor en applikasjon, aka Docker container, skal kjøre. Dette ut i fra gitte constraints som hvor mange instanser av appen som kjøre samtidig, om instansene må kjøre på forskjellige hoster, minne/cpu-bruk, om de må kjøre på samme host som en annen app, etc.

avhengigheter,
helsesjekk
skalering
service discovery
rett og slett orkestrering

----

```
{
    "id": "/finn/reise/flight/web",
    "container": {
        "type": "DOCKER",
        "docker": {
            "image": "tutum.co/stigkj/finn_reise_flight_web",
            "portMappings": [{ "containerPort": 8080, "hostPort": 0}]
    }},
    "env": { "CONSTRETTO_TAGS": "local" },
    "instances": 3,
    "mem": 512.0,
    "dependencies": ["/finn/reise/flight/api"],
    "healthChecks": [{
      "path": "/health", "intervalSeconds": 10,
      "timeoutSeconds": 20, "maxConsecutiveFailures": 3
    }]
}

```

Note:
curl -X POST -H "Accept: application/json" -H "Content-Type: application/json" \
  http://localdocker:8080/v2/apps -d '

----

# Some smaller ones

Note:
Her kommer et bitte lite utvalg av andre verktøy som er litt mer spissede.

----

# Consul

Note:
Denne har egentlig ikke noe med Docker å gjøre, men kan integreres lett. Kort fortalt service discovery og distribuert key-value store

----

# blockade

Note:
Dette er et verktøy for å test nettverks feil og partitions i en distribuert app. Brukes av Alexei for å teste hvordan greenpages håndterer nettverksfeil.

----

# logspout

Note:
Dette er en Docker container som aggregerer logger og kan sende de til en sentral log-server, bl.a.

----

# dind (docker-in-docker)

Note:
Docker-in-docker er en container som klarer å kjøre opp en Docker container inne i seg selv

----

## The Docker Ecosystem
<br/>

http://www.mindmeister.com/389671722/docker-ecosystem

