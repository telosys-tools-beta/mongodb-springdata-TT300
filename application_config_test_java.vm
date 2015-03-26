package org.demo;

import com.mongodb.Mongo;
import cz.jirutka.spring.embedmongo.EmbeddedMongoBuilder;
import org.springframework.context.annotation.Bean;

import java.io.IOException;

public class ApplicationConfigTest extends Application {

    @Bean(destroyMethod="close")
    public Mongo mongo() throws IOException {
        return new EmbeddedMongoBuilder()
                .version("2.4.5")
                .bindIp("127.0.0.1")
                .port(12345)
                .build();
    }

}
