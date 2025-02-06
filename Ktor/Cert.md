```kotlin
https://ktor.io/docs/server-ssl.html#self-signed

ktor:  
  application:  
    modules:  
      - baranfit.ir.ApplicationKt.module  
  deployment:  
    port: 80  
    sslPort: 443  
  
  security:  
    ssl:  
      keyStore: "/root/deploy/keystore.jks"  
      keyAlias: sampleAlias  
      keyStorePassword: 123456  
      privateKeyPassword: 123456
```