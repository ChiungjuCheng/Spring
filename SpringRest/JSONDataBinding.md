---
output: html_document
params: 
    new_title: "My Title!"
title: "``r params$new_title` test paste`"
---
#JSON Data binding
是指讓JSON物件轉換成Java pojo物件，在java內可以使用Jackson套件來做轉換，他只會呼叫setXXX()方法來設定屬性，不會直接使用private file。

####JSON to JAVA POJO and JAVA POJO TO JSON

```java
public class Driver {
    // Jackson物件
    ObjectMapper mapper = new ObjectMapper();

    // 將JSON檔案轉成Java POJO
    Student myStudent = mapper.readValue(new File("/sample.json"), Student.class);

    // 將java 轉成JSON
    mapper.enable(SerializationFeature.INDENT_OUTPUT);
    mapper.writeValue(new File("data/output.json"),myStudnet)
}
```
<mark> 在REST controller中，所有的JSON和Java物件都會透過Jackson套件互相轉換!</mark>