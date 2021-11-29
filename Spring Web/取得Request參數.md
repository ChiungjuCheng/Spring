### 使用@PathVariable

Client端可以透過URL來拿取特定資料，例如
/student/11 拿到座號11的資料
/student/12 拿到座號12的資料


```java

// RESTFul controller

@GetMapping("/students/{studentId}")
public Student getStudent(@PathVariable int studentId) {
    
}

```