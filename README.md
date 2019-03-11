# kafka-zookeeper

Creating statefulsets for kafka and zookeeper
Service for kafka. Type is NodePort \n
kubectl create -f kafka-svc.yml

Statefulset for kafka. Edit the yaml file for KAFKA_ADVERTISED_PORT with NodePort and KAFKA_ADVERTISED_HOST_NAME with NodeIP 
details from the service created
kubectl create -f kafka-dep.yml

Statefulset for zookeeper
kubectl create -f zookeeper.yml

Creating a topic and sending message
kubectl exec -it <pod_name> -- /bin/bash /opt/kafka/bin/kafka-console-producer.sh --broker-list <Node_IP>:<Node_Port> --topic <topic-name>
kubectl exec -it kafka-broker0-0 -- /bin/bash /opt/kafka/bin/kafka-console-producer.sh --broker-list 34.73.88.6:32327 --topic test

Consuming a message
kubectl exec -it <pod_name> -- /bin/bash /opt/kafka/bin/kafka-console-consumer.sh --bootstrap-server <Node_IP>:<Node_Port> --topic <topic-name> --from-beginning
kubectl exec -it kafka-broker0-0 -- /bin/bash /opt/kafka/bin/kafka-console-consumer.sh --bootstrap-server 34.73.88.6:32327 --topic test 
--from-beginning
  
List the topics
kubectl exec -it <pod_name> -- /bin/bash /opt/kafka/bin/kafka-topics.sh --list --zookeeper <zookeeper_clusterIP>:<Cluster_Port(2181)>
kubectl exec -it kafka-broker0-0 -- /bin/bash /opt/kafka/bin/kafka-topics.sh --list --zookeeper 10.103.95.45:2181
