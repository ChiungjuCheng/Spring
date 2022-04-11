# multiple datasources issue
當有多個datasource時，會需要多個DataSourceTransactionManager，而當使用兩個transaction managers時，會導致第一個transaction manager來處理所有的synchronizations ，不論資料原本是屬於第一個或第二個的transactional resources。若第二個 transaction manager commit失敗，而所有synchronizations 都已經處理完後，就沒有辦法可以回復。因此原本用於處理這方面的ChainedTransactionManager 被標註為deprecate。  
看目前資料感覺沒有解決的方法.....
https://github.com/spring-projects/spring-data-commons/issues/2232