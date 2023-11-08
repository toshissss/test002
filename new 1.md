GET spaninfo/_search
{
	"query": {
		"bool": {
			"must": [
				{
					"term": {
						"tags.msgType": {
							"value": "10000002"
						}
					}
				},
				{
					"script": {
							"source": "return doc['tags.price'].value>doc['r=tags.dealPrice'].value",
							"lang": "painless"
					}
				}
			]
		}
	}
}
