---
layout: doc
title: "HTTP qalay isleydi?"
author: "Turdıbek Jumabaev"
updated: "2026-06-29"
topic: "HTTP"
permalink: /
---

Hár kún brauzer arqalı saytlardı ashıw waqıtında sayt atı aldındaǵı "http://" qosımtasına kózimiz túsedi. Biz oǵan derlik itibar bermeymiz. Búgin tolıq dıqqatımızdı HTTP'ge qaratıp, onı úyrenemiz. Ol ne ekenin, qanday waziypa atqarıp turǵanın túsiniwge háreket etemiz. Maqala dawamında tek úyreniw menen sheklenip qalmay, úyrengenlerimizdi bekkemlew ushın ózim 0den HTTP server qurıp kóremiz.

## Protokol ne?

HTTP haqqında sóz baslawdan aldın, protokol haqqında dáslepki túsinik bolǵanı maqul. 
Sebebi HTTP'di tarqatsaq **HyperText Transfer Protocol** boladı, yaǵniy bas tema atınıń ózinde protokol sózi bar. 

Protokol — bul eki tárep aldınnan kelisip alǵan qaǵıydalar. 
Kúndelikli turmısımızda biz sezgen hám sezbegen protokollar kóp, máselen, basqa adamlar menen ortaq tilde sóylesiwimiz. Eger shet elde oqıp atırǵan student mısalında qarasaq ol gruppalasları menen anglichan, 
ata-anası menen qaraqalpaq tilinde sóylesedi. Nege? 
Sebebi jaǵdayǵa qarap, eki tárep ushın ortaq til tańlaw tábiyiy jaǵday. 

Protokolǵa da kompyuterler arasındaǵı ulıwmalıq til dep qarasaq boladı. 
Protokol bolmasa, eki kompyuter bir-birin túsinbeydi, tap ulıwmalıq til bolmaǵan eki adam sıyaqlı. 

## HTTP qay jerde turadı?

Brauzerde `google.com` saytın ashqan waqıtımızda qalayınsha mıńlaǵan kilometr uzaqlıqtaǵı serverdi tawıp, kerekli maǵlıwmattı adaspay, joǵaltpay alıp keledi? Bul qıyın waziypa, sol sebepli bunı HTTP jalǵız ózi qılmaydı, basqalarǵa isenip tapsıradı.

Mısal ushın siz uzaqtaǵı dostıńızǵa xabar jiberiwińiz kerek, xabardı xat arqalı jiberiwge boladı. Qaǵazǵa jazasız, kerekli mánzil hám xattı pochtaǵa tapsırasız, pochta xattı dostıńızǵa alıp barıp beredi. Yaǵniy xabar kerekli jerge barıwı ushın bir-neshe qatlamlardan ótedi. Internet penen de soǵan uqsaslaw jaǵday, ol jerde de hár qıylı waziypalardı atqarıwshı qatlamlar bar. 

Máselen:
  - HTTP — xattıń mazmunı.
  - TCP — pochta xızmeti.
  - IP — mánzil.
  - Fizikalıq qatlam — jol: wi-fi tolqınları, sımlar.

Xat jazǵanda pochta onı qalay jetkerip beriwin oylamaymız. Tap sol sıyaqlı, HTTP haqqında úyrenip atırǵanda da basqa qatlamlar haqqında oylamań.

Keyinlew biz Python'da `socket` ashamız. Socket — bul pochta xızmetine esik. Biz socket arqalı xattı pochtaǵa tapsıramız, pochta — bul TCP. Xat mánzilge jetip barıwın pochta moynına aldı, qalay jetkerip beriwi bizge qızıq emes.

## Kózimiz benen kóremiz

Joqardaǵı gáplerden keyin HTTP haqqında ulıwmalıq túsinik payda bolǵan shıǵar. Endi ámelde qalay bolıwın kóreyik. Bunıń ushın bizge `curl` qosımshasınıń kómegi kerek boladı.

```
curl -v http://example.com
```
```
* Host example.com:80 was resolved.
* IPv6: (none)
* IPv4: 172.66.147.243, 104.20.23.154
*   Trying 172.66.147.243:80...
* Connected to example.com (172.66.147.243) port 80
> GET / HTTP/1.1
> Host: example.com
> User-Agent: curl/8.7.1
> Accept: */*
> 
* Request completely sent off
< HTTP/1.1 200 OK
< Date: Thu, 25 Jun 2026 12:39:25 GMT
< Content-Type: text/html
< Transfer-Encoding: chunked
< Connection: keep-alive
< Server: cloudflare
< Last-Modified: Fri, 19 Jun 2026 18:46:03 GMT
< Allow: GET, HEAD
< Accept-Ranges: bytes
< Age: 13193
< cf-cache-status: HIT
< CF-RAY: a11408f0cd411ae7-WAW
< 
<!doctype html><html lang="en"><head><title>Example Domain</title><link rel="icon" href="data:,"><meta name="viewport" content="width=device-width, initial-scale=1"><style>body{background:#eee;width:60vw;margin:15vh auto;font-family:system-ui,sans-serif}h1{font-size:1.5em}div{opacity:0.8}a:link,a:visited{color:#348}</style></head><body><div><h1>Example Domain</h1><p>This domain is for use in documentation examples without needing permission. Avoid use in operations.</p><p><a href="https://iana.org/domains/example">Learn more</a></p></div></body></html>
* Connection #0 to host example.com left intact
```

Nátiyjedegi "`>`" belgisi menen baslanǵan qatarlar bul biz jibergen request, "`<`" belgisi menen baslanǵan qatarlar bolsa server qaytarǵan juwap. Usı jerden kórsek boladı HTTP soraw-juwaplar ápiwayı tekst, basqa hesh nárse emes.

Yaǵniy HTTP soraw bul tek anıq tártip penen formatlanǵan tekst. Bul tekstte bizdiń soraw tolıq qáliplesken boladı. 

## Anatomiya

Soraw hám juwap anatomiyası dım quramalı emes. Biz de azǵana háreket etsek onı túsinsek boladı. 

HTTP soraw:

```
GET / HTTP/1.1
Host: example.com
User-Agent: curl/8.7.1
Accept: */*
 
```

Máselen soraw 4 bólimnen ibarat:

  1. **Request line** — birinshi qatar: method (`GET`), path (`/`), versiya (`HTTP/1.1`).
  2. **Headers** — "`key: value`" formatındaǵı maǵlıwmatlar.
  3. **Bos qatar** — headers bólimi juwmaqlanǵanın bildiriw ushın.
  4. **Body** — ádette GET sorawında body bolmaydı.

Juwap penen de usıǵan uqsas jaǵday, onı da eplep túsine alamız.

HTTP juwap:

```
HTTP/1.1 200 OK
Date: Thu, 25 Jun 2026 12:39:25 GMT
Content-Type: text/html
Transfer-Encoding: chunked
Connection: keep-alive
Server: cloudflare
Last-Modified: Fri, 19 Jun 2026 18:46:03 GMT
Allow: GET, HEAD
Accept-Ranges: bytes
Age: 13193
cf-cache-status: HIT
CF-RAY: a11408f0cd411ae7-WAW
 
!doctype html><html lang="en"><head><title>Example Domain</title><link rel="icon" href="data:,"><meta name="viewport" content="width=device-width, initial-scale=1"><style>body{background:#eee;width:60vw;margin:15vh auto;font-family:system-ui,sans-serif}h1{font-size:1.5em}div{opacity:0.8}a:link,a:visited{color:#348}</style></head><body><div><h1>Example Domain</h1><p>This domain is for use in documentation examples without needing permission. Avoid use in operations.</p><p><a href="https://iana.org/domains/example">Learn more</a></p></div></body></html>
```

Bul jerde:

  1. **Status line** — versiya, status kod (`200`), sebep (`OK`).
  2. **Headers** — sorawdaǵı sıyaqlı.
  3. **Bos qatar** — sorawdaǵı sıyaqlı.
  4. **Body** — haqıyqıy mazmun, ádette HTML kod yamasa JSON obyekt.

## Serverimizdi quramız

Bizde HTTP haqqında túsinik bar, soraw hám juwap anatomiyasın da úyrenip aldıq. Demek óz HTTP serverimizdi jazıp kóriwge hesh nárse tosqınlıq etpeydi. Onda neni kútip turmız? Jazıp kórmedik pe!?

Joqarda soket haqında sóz ashqan edik. Biz soket arqalı TCP'ge tekst beremiz, jetkeriwdi TCP bejeredi.

<div class="callout">
  <div class="callout-label">ESKERTPE</div>
  <p>Maqala dawamında kod Python tilinde jazıladı. Eger siz Python'dı bilmeytuǵın bolsańız mashqala emes. Internetti azǵana astan-gesten qılıp ózińiz bilgen qálegen programmalastırıw tilinde jazsańız boladı.</p>
</div>

Server kodı (`server.py`):

Python tilinde soketler menen islesiw ushın tayyar ishki kitapxana bar, biz sodan paydalanamız:

```
import socket
```

Jańa soket obyektin jaratamız:

```
server = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
```

Kodtaǵı `socket.AF_INET` — IPv4 mánzilinen paydalanıwdı, `socket.SOCK_STREAM` — TCP protokolın tańlaǵanımızdı ańlatadı.

Soketti arnawlı sazlaw:

```
server.setsockopt(socket.SOL_SOCKET, socket.SO_REUSEADDR, 1)
```

Bazı waqıtları serverdi óshirip, tez qayta iske túsirsek "Address already in use" yaǵniy "Mánzil bánt" degen qátelik shıǵadı. Ol bizge kerek emes, sol ushın `SO_REUSEADDR` arqalı porttı qayta paydalanıwǵa ruqsat beremiz.

Serverdi belgili bir IP mánzil hám portqa biriktiremiz:

```
server.bind(("127.0.0.1", 8080))
```

"`127.0.0.1`" — bul lokal kompyuterimiz, yaǵniy "`localhost`", "`8080`" — bolsa tarmaqtaǵı port.

Bizde server birew, biraq klientler kóp bolıwı múmkin. Bazı waqıtları bir qansha klientler bir waqıtta jalǵanıp qalıw itimallıǵı bar. Bunday jaǵdayda biz hár bir <i>connection</i>di gezek penen qabıllaymız. Server bir <i>connection</i> menen bánt bolıp turǵanda, keynen kelgenler náwbette turıwı kerek. Tómendegi kod arqalı náwbet uzınlıǵın belgilep beremiz:

```
server.listen(5)
```

Server iske túskenligi haqqında xabardı konsolǵa shıǵaramız, bul tek ózimiz ushın:

```
print("Server iske tústi: http://127.0.0.1:8080")
```

Endi biz sorawlardı qabıl etiwge tayarmız. Bunı sheksiz cikl arqalı ámelge asıramız:

```
while True:
    conn, addr = server.accept()

    request = conn.recv(4096)
    print(request.decode("utf-8", errors="replace"))

    body = "Sálem álem!"
    response = (
        "HTTP/1.1 200 OK\r\n"
        "Content-Type: text/plain; charset=utf-8\r\n"
        f"Content-Length: {len(body.encode('utf-8'))}\r\n"
        "\r\n"
        f"{body}"
    )

    conn.sendall(response.encode("utf-8"))
    conn.close()
```

Sheksiz cikl paydalanǵanımızdıń sebebi biziń server turaqlı islep turıwı kerek. Bul arqalı klientlerden kelgen sorawlardı toqtawsız qabıl qılıwımız múmkin. 

`conn, addr = server.accept()` — klient (máselen brauzer) serverge jalǵanıwın kútedi. Jalǵanıw ámelge asqanda eki mánis qaytadı:
  - conn — klient penen maǵlıwmat almasıw ushın jańa soket obyekti.
  - addr — klienttiń IP mánzil hám portı.

Klient jibergen sorawdı bizge TCP aǵım ("stream") retinde jiberedi — bul úzliksiz baytlar aǵıp kiyatırǵan dáryaǵa uqsaydı. Agıp kelgen maǵlıwmatlar soket bufferinde jıynalaberedi. `recv(4096)` metodın shaqırıw arqalı sol bufferden eń kóbi menen 4096 bayt alınıwın belgilep beremiz. Eger klientten 4096 bayttan úlken request kelse biz tek 4096 baytın ǵana oqıymız, qalǵanı hesh jaqqa joǵalmaydı, soket bufferinde turaberedi.

Bul jerde 4096 qatıp qalǵan san emes, ózińizden kelip shıǵıp qálegen sandı jazsańız boladı. Ádette 2 niń dárejelerindegi san jazıladı, máselen: 1024, 2048, 4096 yamasa 8192. Ápiwayı GET sorawı onsha úlken bolmaǵanı ushın biz 4096nı maksimum dep belgiledik. 

Soketten kelgen maǵlıwmat mudamı baytlar kórinisinde boladı — sebebi tarmaq arqalı tek baytlar almasınadı, tekst emes. Bizge tekst (`str`) kerek, sol ushın bayttı tekstke aylandırmız, mine usı nárse "dekod qılıw" delinedi. 

Dekod qılıwshı kod: `decode("utf-8", errors="replace")`

  - "`utf-8`" — qaysı kadirovka tiykarında baytlardı háriplerge aylandırıwdı belgileydi. Nege UTF-8? Sebebi UTF-8 internette eń keń tarqalǵan kadirovkalardan biri. Bul kadirovkada bizge kerek barlıq latın-kiril háripleri hám emojiler bar. 
  - "`errors="replace"`" — eger baytlar arasında UTF-8 ge durıs kelmeytuǵın bayt ushrasa ne qılıw kerek ekenin belgileydi. Standart jaǵdayda (`errors="strict"`) buzıq bayt ushrasa programma qátelik shıǵarıp, islewden toqtaydı. Biz "replace" arqalı "toqtama, buzıq baytti arnawlı belgi (`�`) menen almastır hám dawam et" degen buyrıqtı beremiz.

Endi juwap qaytarıwımız kerek. `body = "Sálem álem!"` — ekranda kóriniwi kerek bolǵan tekstti ózgeriwshige saqlap alamız. Kod dawamında `response` ózgeriwshisi jaratılǵan. Onıń mánisine itibar bersek, tap biz joqarda úyrengen juwap anatomiyası menen birdey status line, headers, bos qatar hám body bólimlerin kóremiz.

`conn.sendall()` arqalı juwaptı jiberemiz hám `conn.close()` arqalı baylanısti úzip, barlıǵın juwmaqlaymız.

Server kodın jazıp boldıq, endi iske túsirip tekserip kórsek boladı.

## Serverdi iske túsirip, tekseremiz

Server islewi ushın kompyuterimizge Python ornatılǵan bolsa bolǵanı, tómendegi buyrıq arqalı serverimizdi iske túsiriw múmkin:

```
python3 server.py
```

Nátiyje:
```
Server iske tústi: http://127.0.0.1:8080
```

Endi brauzerde `http://127.0.0.1:8080` mánzilin ashıp kórsek boladı:

<figure>
  <img src="/assets/images/helloworld.png" alt="1-súwret: brauzerde ashılǵan jaǵday">
  <figcaption>1-súwret: brauzerde ashılǵan jaǵday</figcaption>
</figure>

`curl` menen de soraw jiberip kórsek boladı:

```
curl -v http://127.0.0.1:8080/
```

Nátiyje:

```
*   Trying 127.0.0.1:8080...
* Connected to 127.0.0.1 (127.0.0.1) port 8080
> GET / HTTP/1.1
> Host: 127.0.0.1:8080
> User-Agent: curl/8.7.1
> Accept: */*
> 
* Request completely sent off
< HTTP/1.1 200 OK
< Content-Type: text/plain; charset=utf-8
< Content-Length: 13
< 
* Connection #0 to host 127.0.0.1 left intact
Sálem álem!
```

Yashaqay! Serverimiz iske tústi hám biz kútkendey islemekte...

## Sońı

Maqala basında maqsetimiz HTTPdi jaqsı túsiniw hám óz HTTP serverimizdi jazıp kóriw edi. Menińshe biz maqsetimizge jettik. Eger berilgen maǵlıwmatlardı tolıq túsinip ózlestirgen, server kodın jazıp, iske túsirip hám teksergen bolsańız — qutlıqlayman! Bul haqıyqatında da maqtanıwǵa arzıytuǵın nátiyje. Sebebi bunıń barlıǵı web qalay isleytuǵının túsindiredi, siz jazǵan HTTP server — web freymworklardıń negizin kórsetip bere aladı.

## Tapsırma

Alǵan bilimlerińizdi bekkemlew ushın tómendegi wazıypalardı orınlap kóriwdi usınıs etemen:

  1. Juwaptı ózgertiń. Body'ǵa basqa teskt jazıń hám HTML kodtı juwap retinde qaytarıp kórin — brauzerde qanday kórinedi eken?
  2. `recv`ke kishi san beriń. Máselen 4096nı 10ǵa ózgertip, curl arqalı soraw jiberiń hám qaytqan juwaptı dıqqat penen analiz qılıń.
  3. `Content-Length` mánisin bilip turıp qáte berip kóriń.
  4. Sorawǵa qarap hár qıylı juwap qaytarıń. Házir server qálegen sorawǵa birdey juwap qaytaradı. Biraq izde `path`ge qarap juwap qaytarıw imkaniyatı bar. Joqarda úyrengen soraw anatomiyasın esleń. Sol jerde path haqqında aytılǵan. 
  Tómendegishe islesin:

  - `/` ushın — "Sálem álem!" teksti.
  - `/about` ushıń — "Biz haqqında" teskti.
  - Basqa hár qanday path ushın — `404 Not Found` juwabı qaytsın.


<figure>
  <img src="/assets/images/homepage.png" alt="2-súwret: bas bet">
  <figcaption>2-súwret: bas bet</figcaption>
</figure>

<figure>
  <img src="/assets/images/aboutpage.png" alt="3-súwret: biz haqqında beti">
  <figcaption>3-súwret: biz haqqında beti</figcaption>
</figure>

<figure>
  <img src="/assets/images/pagenotfound.png" alt="4-súwret: bet tabılmadı">
  <figcaption>4-súwret: bet tabılmadı</figcaption>
</figure>

