# @ExceptionHandler
```java
@ExceptionHandler
public ResponseEntity<APIErrorResponse> general(RuntimeException e) {
  return ResponseEntity.internalServerError().build();
}

// 여러개의 에러를 잡고싶을 때
@ExceptionHandler({RuntimeException.class, IOException.class})
public ResponseEntity<APIErrorResponse> general(Exception e) {
  return ResponseEntity.internalServerError().build();
}
```
# @ControllerAdvice
- @ExceptionHandler를 모아서 글로벌하게 적용할 때 쓰는 어노테이션
  - 종류
    - @ControllerAdvice
    - @RestControllerAdvice = @ControllerAdvice + @ResponseBody
  - 속성
    - value == basePackages
    - basePackages: 적용 범위를 문자열을 이용해 특정 패키지로 지정
    - basePackageClasses: 적용 범위를 대표 클래스 한 개를 이용해 특정 패키지로 지정
      - basePackages를 type-safe 하게 사용하기 위해서 제공하는 옵션
    - assignableTypes: 적용 범위를 특정 클래스에 할당할 수 있는 컨트롤러로 지정
    - annotations: 적용 범위를 특정 어노테이션을 사용한 컨트롤러로 지정
## ResponseEntityExceptionHandler
- Spring MVC에서 내부적으로 발생하는 예외들을 처리하는 클래스
  - API 예외 처리를 담당하는 @ControllerAdvice 클래스에서 상속 받아 사용
  - 커스터마이징을 원하는 특정 메소드를 오버라이드
