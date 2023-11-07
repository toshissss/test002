# test002
test-search-workplace


###测试test
# Sample Logstash configuration for creating a simple
# Beats -> Logstash -> Elasticsearch pipeline.

input {
  file {
    path => ["D:/ES_hq/csv/*.csv"]
	start_position => "beginning"
  }
}

filter {
 
  csv {
    separator => ","
	skip_header => true
#	autodetect_column_names => "true"
    columns => ["no","date","opening","closing","fluctuations","fluctuations_percent","lowest","highest","deal_hands","deal_amount","ratio","turnover_rate","code","market","next_day","next_closing","next_opening","next_lowest","next_highest"]
    remove_field => ["message","host", "@timestamp", "@version","event","log.file.path"]
  }	
  ##新增字段去掉单引号’
  mutate {
	gsub => [
		"code", "'", ""
	]
  }
}


output {   
 elasticsearch {
    hosts => ["https://172.168.0.100:9200","https://172.168.0.101:9200","https://172.168.0.102:9200","https://172.168.0.104:9200","https://172.168.0.105:9200"]
    index => "stock-market-prediction-000002"
    user => "elastic"
    password => "z_*sesa=J9fKdnZ95U1O"
    ssl => "true"
    cacert => "D:/0914shujuguandao/logstash-8.5.3/logstash-8.5.3/http_ca.crt"
	pipeline => "%{market}_%{code}_next_day_prediction"
  }
  stdout{}
}



