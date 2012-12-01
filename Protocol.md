Paths:
=====
/offer

HTTP POST 
request
{
	"id":"<cell-number>",
	"path":[
	{
		"name":"<title>",
		"lat":"<lat>",
		"long":"<long>"
	}
	..
	]
	"vehicleType":"<vehicleType>",
	"places":"<numberOfPlaces>",
	"startTime":"<DateTimeStamp>",
	"endTime":"<DateTimeStamp>",
}

response


Note:
- inizialmente il path e' un array con due oggetti: origine e destinazione
- quando mi arriva la notifica push, avro' una richiesta con una lista di oggetti "tappe"
- dopo la notifica push l'orgine e' aggiornata alla nuova posizione corrente


/request