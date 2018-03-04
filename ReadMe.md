#   Usage (All are mvn and are springboot applications)
    -   Download the zip or clone the Git repository.
    -   Unzip the zip file (if you downloaded one)
    -   Open Command Prompt and Change directory (cd) to folder containing pom.xml
    -   Open Eclipse: File -> Import -> Existing Maven Project -> Navigate to the folder where you unzipped the zip
    -   Select the right project
    -   Choose the Spring Boot Application file (RestfulWebServicesApplication.java)
    -   Right Click on the file and Run as Java Application

#   Spring Microervices:
    # Characteristics
    -   They are small components
    -   Each microservice is independently deployable
    -   Simple communication (typically HTTP)
    -   They are stateless (can be dynamically scaled up or scaled down)
    -   Automated Build and Deployment

#   Challenges
    -	Bounded Context (Understanding the boundary for micro services)
    -	 Configuration Management 
    -	Manage configuration to dynamically scale up/down
    -	Visibility (Managing the health of micro services
	-	Pack of Cards (Build fault tolerance)
 
#   Spring Cloud 
    Spring Cloud provides tools for developers to quickly build some of the common patterns in distributed systems (e.g. configuration
    management, service discovery, circuit breakers, intelligent routing, micro-proxy, control bus, one-time tokens, global locks, leadership election,
    distributed sessions, cluster state). Coordination of distributed systems leads to boiler plate patterns, and using Spring Cloud developers can quickly stand
    up services and applications that implement those patterns. They will work well in any distributed environment, including the developer's own laptop, bare
    metal data centres, and managed platforms such as Cloud Foundry.
 
#   Components Used
    -   Naming Server (Eureka)
    -   Ribbon (Client Side Load Balancing)
    -   Feign (Easier REST Clients)

#   Visibility and Monitoring
    -   Zipkin Distributed Tracing Server
    -   Netflix API Gateway
    
#   Fault Tolerance
    -   Hystrix
 
#   Advantages of Micro Services
    -   Adaption of new technologies and processes
    -   Dynamic Scaling
    -   Faster Release Cycles

#   High level flow:
    -   limits-service <--> spring-cloud-config-server --> Git
    
#   limits-service (A simple springboot application)
    -   Bootstrap "spring-cloud-config-server" with it's url (http://localhost:8888/limits-service/default or dev or qa) from bootstrap.properties
    -   http://localhost:8080/limits
    -   This should pick up the configuration from "spring-cloud-config-server" from git repo.
    
#   spring-cloud-config-server    
    -   Install local git from (https://git-scm.com/)
    -   Create Local repo: 
        -   mkdir git-localconfig-repo
        -   cd /exercise/udemy/microservices/git-localconfig-repo
        -   git init
        -   go to eclipse, right click on: spring-cloud-config-server
        -   Build Path -> Link Source -> Browse and select  git-localconfig-repo
    -   http://localhost:8888/limits-service/default or dev or qa
    -   The order of the configuration is as configured in it's specific properties, the fall back is "default", which is application.properties

#   currency-exchange-service    
    -   http://localhost:8000/currency-exchange/from/USD/to/INR
    -   http://localhost:8001/currency-exchange/from/USD/to/INR (Configure the port as env. variable)
    -   http://localhost:8000/h2-console/login.jsp?jsessionid=80ee91dbb22360ee81dda119b322b250

#   currency-conversion-service
    -   http://localhost:8100/currency-converter/from/USD/to/INR/quantity/1000
    
#   Feign (Calling Currency Exchange Service from Currency Calculation Service using Feign as Proxy)
    -   Feign makes it easy to invoke other restful services.
    -   It provides integration with Ribbon, which is a client side load balancer.  
    -   http://localhost:8100/currency-converter-feign/from/USD/to/INR/quantity/1000

#   netflix-eureka-naming-server
    -   Offers Service registration and service discovery feature
    -   http://localhost:8761/
    
#   netflix-zuul-api-gateway-server (Zuul: API Gateway)
    -   http://localhost:8765/currency-exchange-service/currency-exchange/from/EUR/to/INR -- accessing directly
    -   http://localhost:8100/currency-converter-feign/from/EUR/to/INR/quantity/10000 -- going through Feign
    -   http://localhost:8765/currency-conversion-service/currency-converter-feign/from/EUR/to/INR/quantity/10000  
        (Invoking the above URL, will first hit zuul proxy server and the again when conversion service talks exchange service)
    -   Authentication, authorization and security
    -   Rate Limits
    -   Fault Tolerance
    -   Service Aggregation
    
#   Spring Cloud Sleuth   
     -   It implements a distributed tracing solution for Spring Cloud, borrowing heavily from Dapper, Zipkin and HTrace. For most
         users Sleuth should be invisible, and all your interactions with external systems should be instrumented automatically. You can capture
         data simply in logs, or by sending it to a remote collector service.
    
#   zipkin-distributed-tracing-server (Zipkin Distributed Tracing)
    -   Zipkin is a distributed tracing system. It helps gather timing data needed to troubleshoot latency problems in microservice architectures. 
        It manages both the collection and lookup of this        data. Zipkin’s design is based on the Google Dapper paper.
    -   Microservices --> RabbitMQ --> ZipkinDistributedTracingServer --> Database: Visualize using Zipkin UI.
    #   Install Rabbit MQ: 
        -   https://www.rabbitmq.com/install-homebrew.html
        -   brew update
        -   brew install rabbitmq
        -   The RabbitMQ server scripts are installed into /usr/local/sbin.. so you may wish to add export PATH=$PATH:/usr/local/sbin to your .bash_profile
        -   To start the server: rabbitmq-server.
        -   http://localhost:15672
        -   Username/password: guest/guest (The broker creates a user guest with password guest.)
     -  http://localhost:9411/zipkin/   
    
#   Spring Cloud Bus Over RabbitMQ
    -   http://localhost:8080/bus/refresh
    
#   Fault Tolerance with Hystrix



    


