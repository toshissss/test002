for i in {1..10};
doqeqeq

		echo "##每十秒执行一次，统计写入reject"
        #curl 168.11.225.87:19200/_cat/thread_pool/write >> file.txt
        curl -u elastic:elastic 172.168.0.96:9200/_cat/thread_pool/write >> text.txt
		echo "-----10s----" >> text.txt
        sleep 10s
        
done


