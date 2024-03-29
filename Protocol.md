Paths:
=====

Risorsa: percorso
-----------------

/paths/<phoneNumber>
sempre vuota, se e' cambiata

response
{
	("pathResponse":"<link-routing-XML>")
}

Risorsa: offer
--------------

create new offer
POST 
/offers

request
{
	"idUtente":"<cell-number>",
	"userName":<user-name>,
	"pathRequest":[
	{
		"name":"<title>",
		"lat":"<lat>",
		"long":"<long>"
	}
	..
	]
	"vehicleType":"<vehicleType>",
	"places":"<numberOfPlaces>",
	"requestTime":"<DateTimeStamp>",
	"startOrEnd":"<true|false>",
	"maxThreshold":"<numberOfSeconds>"
}

response
{
	"idOffer":"<id-DB>",
	"idUtente":"<cell-number>",
	"pathResponse":"<link-routing-XML>"
}

Note:
- inizialmente il path e' un array con due oggetti: origine e destinazione
- quando mi arriva la notifica push, avro' una richiesta con una lista di oggetti "tappe"


update offer (quella che arriva dalla push notification)
POST 
/offers/<id-offer>

request
{
	"idUtente":"<cell-number>",
	"userName":<user-name>,
	"pathRequest":[
	{
		"name":"<title>",
		"lat":"<lat>",
		"long":"<long>"
	}
	..
	]
	"vehicleType":"<vehicleType>",
	"places":"<numberOfPlaces>",
	"requestTime":"<DateTimeStamp>",
	"startOrEnd":"<true|false>"
}

response
{
	"idOffer":"<id-DB>",
	"idUtente":"<cell-number>",
	"pathResponse": "<link-routing>"
}

Note:
- dopo la notifica push l'orgine e' aggiornata alla nuova posizione corrente

take offer
POST 
/offers/<phoneNumber>/join

Note:
- cristallizza l'offerta
- (comporta che abbasso il numero di persone disponibili )
- scatena PUSH NOTIFICATION con link al quale andare


GET
/offer?orderBy=<typeOfOrder>&limit=<limit>&offset=<offset>

response
[
{
	(offerte di passaggio)
}
]


Lista delle offerte di passaggio

/requests
---------

HTTP POST
request
{
	"idUtente":"<cell-number>",
	"userName":<user-name>,
	"numberOfPerson":"<number>",
	"pathRequest":[
	{
		"name":"<title>",
		"lat":"<lat>",
		"long":"<long>"
	}
	..
	]
	"friends":[
	{
		"name":"<name>",
		"phoneNumber":"<cell>"
	}
	]
}

(order by: ritardo dovuto al passagio ASC)
response {
	"idUtente":"<idUser>",
	"username":"name",
	"offers":[
	{
		"userName":"<name>",
		"phoneNumber":<cell>,
		"vehicleType":"<vehicleType>",
		"waitingTime":"<waitingTime>"
	}
	]	
}