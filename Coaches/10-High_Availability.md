# High availability

## Progress Diagram

![Final progress diagram](/images/final-progress-diagram.jpg)

## Happy Path

* Edit CosmosDB with multi master or at least geo-replication with secondary read to a second region
* Deploy the same functions code to a second region
* Add Traffic Manager in front of them
