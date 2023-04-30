The KafkaConnector class to configure the SSL connection to Kafka.

This example shows how to use the KafkaConnector class to configure the SSL connection to Kafka using the keystore and truststore passwords retrieved from AWS secret-manager:
```java
import io.smallrye.reactive.messaging.kafka.KafkaConnector;
import org.eclipse.microprofile.config.inject.ConfigProperty;

import javax.inject.Inject;

public class KafkaSslExample {

    @Inject
    @ConfigProperty(name = "kafka.ssl.keystore.location")
    String keystoreLocation;

    @Inject
    @ConfigProperty(name = "kafka.ssl.keystore.password")
    String keystorePassword;

    @Inject
    @ConfigProperty(name = "kafka.ssl.truststore.location")
    String truststoreLocation;

    @Inject
    @ConfigProperty(name = "kafka.ssl.truststore.password")
    String truststorePassword;

    public void configureKafkaSsl() {
        KafkaConnector connector = KafkaConnector.create()
                .with("ssl.keystore.location", keystoreLocation)
                .with("ssl.keystore.password", keystorePassword)
                .with("ssl.truststore.location", truststoreLocation)
                .with("ssl.truststore.password", truststorePassword);

        // use the connector to configure the Kafka client
    }
}
```
In this example, we’re using the @ConfigProperty annotation to inject the keystore and truststore locations and passwords from the application’s configuration. You can replace these values with the ones retrieved from AWS secret-manager using the code snippet I provided earlier.

Then, we’re using the KafkaConnector class to build a configuration object that contains the SSL settings for the Kafka
