# @PathVariable

REST API에서 많이 사용한다.

```java
@GetMapping("/{postId}/comments")
public List<Comment> getComments(@PathVariable Long postId) {
    Post myPost = postService.findById(postId);
    return myPost.getCommentList();
}
```

RequestMapping의 value 내에서 {} 사이에 변수명을 넣는다.

그리고 해당 변수명을 갖는 변수로 PathVariable을 불러온다.



정규식도 사용가능

```java
@GetMapping("/{postId:[0-9]*}/comments")
//{id:[A-Z]*} 식으로도 사용가능
```



## 참조

Optional PathVariable

https://howtodoinjava.com/spring-mvc/optional-pathvariable/