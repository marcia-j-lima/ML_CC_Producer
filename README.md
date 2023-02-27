# ML_CC_Producer
Using OAuth in Confluent Cloud

Based on https://developer.confluent.io/get-started/java/#build-producer 

# Create a properties file, let's say oauth.properties:

bootstrap.servers=<CC cloud url for instance>
security.protocol=SASL_SSL
sasl.oauthbearer.token.endpoint.url=https://{your okta dev server}/oauth2/default/v1/token
sasl.login.callback.handler.class=org.apache.kafka.common.security.oauthbearer.secured.OAuthBearerLoginCallbackHandler
sasl.mechanism=OAUTHBEARER
sasl.jaas.config=org.apache.kafka.common.security.oauthbearer.OAuthBearerLoginModule required clientId='{clientId}' clientSecret='{client secret}' scope='{scope}' extension_logicalCluster='{your cluster id}' extension_identityPoolId='{your id pool}';

# Additional config for producer
acks=all
key.serializer=org.apache.kafka.common.serialization.StringSerializer
value.serializer=org.apache.kafka.common.serialization.StringSerializer
key.deserializer=org.apache.kafka.common.serialization.StringDeserializer
value.deserializer=org.apache.kafka.common.serialization.StringDeserializer

# Terminal in Intellij
1. gradle build
2. gradle shadowJar 
3. java -cp build/libs/kafka-java-getting-started-0.0.1.jar producer.CCProducer oauth.properties      