enter mongo shell and create transactions db:

```
$ mongo
> use transactions
```

Create a function to generate random data:

```
> var txs = []
> for (var x = 0; x < 1000 ; x++) {
 var transaction_types = ["credit card", "cash", "account"];
 var store_names = ["edgards", "cna", "makro", "picknpay", "checkers"];
 var random_transaction_type = Math.floor(Math.random() * (2 - 0 + 1)) + 0;
 var random_store_name = Math.floor(Math.random() * (4 - 0 + 1)) + 0;
 txs.push({
   transaction: 'tx_' + x,
   transaction_price: Math.round(Math.random()*1000),
   transaction_type: transaction_types[random_transaction_type],
   store_name: store_names[random_store_name]
   });
 }
```

Write the data to a collection:

```
> db.purchases.insert(txs)
BulkWriteResult({
	"writeErrors" : [ ],
	"writeConcernErrors" : [ ],
	"nInserted" : 1000,
	"nUpserted" : 0,
	"nMatched" : 0,
	"nModified" : 0,
	"nRemoved" : 0,
	"upserted" : [ ]
})
```

Look at 10 documents:

```
> db.purchases.find().limit(10)
{ "_id" : ObjectId("5cb1a49d3e0a85b364fc4aff"), "transaction" : "tx_0", "transaction_price" : 412, "transaction_type" : "credit card", "store_name" : "edgards" }
{ "_id" : ObjectId("5cb1a49d3e0a85b364fc4b00"), "transaction" : "tx_1", "transaction_price" : 738, "transaction_type" : "credit card", "store_name" : "edgards" }
{ "_id" : ObjectId("5cb1a49d3e0a85b364fc4b01"), "transaction" : "tx_2", "transaction_price" : 925, "transaction_type" : "cash", "store_name" : "edgards" }
{ "_id" : ObjectId("5cb1a49d3e0a85b364fc4b02"), "transaction" : "tx_3", "transaction_price" : 509, "transaction_type" : "cash", "store_name" : "cna" }
{ "_id" : ObjectId("5cb1a49d3e0a85b364fc4b03"), "transaction" : "tx_4", "transaction_price" : 380, "transaction_type" : "account", "store_name" : "picknpay" }
{ "_id" : ObjectId("5cb1a49d3e0a85b364fc4b04"), "transaction" : "tx_5", "transaction_price" : 158, "transaction_type" : "credit card", "store_name" : "cna" }
{ "_id" : ObjectId("5cb1a49d3e0a85b364fc4b05"), "transaction" : "tx_6", "transaction_price" : 342, "transaction_type" : "cash", "store_name" : "edgards" }
{ "_id" : ObjectId("5cb1a49d3e0a85b364fc4b06"), "transaction" : "tx_7", "transaction_price" : 832, "transaction_type" : "credit card", "store_name" : "picknpay" }
{ "_id" : ObjectId("5cb1a49d3e0a85b364fc4b07"), "transaction" : "tx_8", "transaction_price" : 841, "transaction_type" : "cash", "store_name" : "picknpay" }
{ "_id" : ObjectId("5cb1a49d3e0a85b364fc4b08"), "transaction" : "tx_9", "transaction_price" : 263, "transaction_type" : "cash", "store_name" : "checkers" }
```
