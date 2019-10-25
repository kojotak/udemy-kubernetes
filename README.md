# udk8s
My notes and examples from Udemy's Docker and Kubernetes course: https://www.udemy.com/course/docker-and-kubernetes-the-complete-guide

## Section 2 - správa kontajnerů
* Docker ps
  * Ukaž běžící kontajery
* Docker ps -all
  * Ukaž všechny kontajnery
* Docker create
  * Vytvoří nový kontajner
* Docker start abc123
  * Spustí vytvořený kontajner s daným ID
* Docker kill abc123
  * Zabije, tedy okamžitě ukončí kontajner s daným ID
* Docker stop abc123
  * Zkusí zastavit kontajner a po 10s ho zabije, pokud se nezastaví
* Docker run
  * Vytvoří a spustí, to stejné jako docker create a docker start
* Docker run busybox ls
  * Pustí příkaz ls ve spuštěném kontajneru busybox
* Docker exec -it abc123 command
  * Připoj se ke kontajneru a vykonej v něm command a interaktivně připoj std in+out
* Docker exec -it abc123 sh
  * Připoj se ke kontajneru a spusť v něm příkazovou řádku
* Docker run -it busybox sh
  * Spusť kontajner a v něm spusť příkazovou řádku

## Section 3 - custom docker images
* Docker build .
  * V adresari s dockerfile vytvori image a vrati ID pro pouziti v docker run
  * FROM - z ceho se ma image odvodit
  * RUN - co se ma pustit za prikaz pro vytvoreni image, muze byt vicekrat
  * CMD - co se ma udelat po spusteni
* Docker build -t dockerid/project:version
  * Vytvori tag, ktery je pak mozne pouzit misto ID
* Dockerid - moje ID z registrace
  * Jako version je mozne pouzit latest

## Section 4 - making real projects
* Copy <from> <to>
  * Uvnitr Dockerfile presune soubory filesystemu dovnitr docker image
* Docker run -p <INCOMING_PORT> : <KONTAJNER_PORT> <imagename>
  * Přesměruje incomming port z localhostu dovnitř kontajneru na kontajner_port
* Workdir /usr/app
  * Uvnitr Dockerfile nastavi prefix pro operace jako je COPY, aby se omylem neprepsal filesystem base image myma souborama
* Na pořadí příkazů v Dockerfile hodně záleží - aby se využila cache!

## Section 5 - docker-compose - multiple local containers
* Docker-compose.yml
  * Umožňuje si uložit opakované příkazy, např. Docker build a docker run
  * Při deklaraci services se použije to samé síťování, takže z příkladu ‘visits’ node-app uvidí redis.Je jen potřeba místo domain:port použít service name z docker-compose souboru
* Docker-compose up --build
  * Všechno přebuildí a spustí všechny kontajnery popsané v yml
* Docker-compose up -d
  * Přebuildí a hodí se do pozadí
* Docker-compose down
  * Vypne všechny kontajnery
* Restart: always
  * Uvnitr docker-compose.yml zpusobi restart kontajneru - vhodne pro webserver
  * Dalsi restart policies: on-failure, no, unless-stopped
* Docker-compose ps
  * Vypíše běžící kontajnery podle yml z aktuálního adresáře
  * Nevypíše nic, pokud v . žádný yml není


