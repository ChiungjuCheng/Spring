# multiple datasources issue
當有多個datasource時，會需要多個DataSourceTransactionManager，而當使用兩個transaction managers時，會導致第一個transaction manager來處理所有的synchronizations ，不論資料原本是屬於第一個或第二個的transactional resources。若第二個 transaction manager commit失敗，但所有的Transaction  synchronizations (備註)都已經處理完後，就沒有辦法可以回復。因此原本用於處理這方面的ChainedTransactionManager 被標註為deprecate。  
看目前資料感覺沒有解決的方法.....  
https://github.com/spring-projects/spring-data-commons/issues/2232

[API deprecate解釋](https://docs.spring.io/spring-data/commons/docs/current/api/org/springframework/data/transaction/ChainedTransactionManager.html)

**備註: Transaction  synchronizations**  
Transaction Synchronization : You can think of this as Spring's TransactionSynchronization interface which receives callback for transaction synchronization..It has various methods like afterCommit(), afterCompletion(),beforeCommit() which get called as per transaction's state..Consider a practical example where you want to send an email to user once user registration is completed ,notify any external service depending on transaction state or log any particular event..  
[節錄來源](https://stackoverflow.com/questions/45266595/transaction-synchronization-vs-transaction-association-in-jpa)