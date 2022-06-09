# @RequestParam

검색 또는 페이징에서 많이 쓰는 것 같다

```
localhost:8080/api?param1=10&param2=20
```

이런 경우에 @RequestParam을 받아와서 처리한다

null 값의 처리가 PathVariable보다는 유연하다.

```java
@GetMapping("/api")
    public String hello(@RequestParam int param1, @RequestParam int param2) {
```



required = true

defaultValue = "value"



요청 파라미터를 Map으로 조회하는 것도 가능하다

@RequestParam



MutlfiValueMap으로도 조회할 수 있다.

