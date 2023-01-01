### 1. 정적 컨텐츠
- 파일을 그대로 웹 브라우저에 전달하는 방식
- `src > main > resources > static`에 .html 파일을 만들어서 작성
- 실행

- body에 작성한 내용이 그대로 웹 브라우저에 반환됨

### 2. MVC & 템플릿 엔진
- HTML을 서버에서 프로그래밍해서 동적으로 변경하여 전달하는 방식 (최근에는 대부분 이 방식을 사용)
- Controller : `src > main > java > project > controller`에 각 컨트롤러 파일 만들어서 작성
```java
@Controller // 어노테이션 붙여주기
public class HelloController {

    @GetMapping("hello-mvc")
    // 파라미터로 넘겨줌
    public String helloMvc(@RequestParam("name") String name, Model model) {
        model.addAttribute("name", name);
        return "hello-template";
    }
}
```
- View : `src > main > resources > templates`에 .html 파일 만들어서 작성
```html
<html xmlns:th="http://www.thymeleaf.org">
<body>
<p th:text="'hello ' + ${name}">hello! empty</p>
</body>
</html>
```
- 실행


### 3. API
- json 데이터 포맷으로 클라이언트에게 데이터를 전달하는 방식
- @ResponseBody 를 사용하고, 객체를 반환하면 객체가 JSON으로 변환됨
- Controller : `src > main > java > project > controller`에 각 컨트롤러 파일 만들어서 작성
```java
    @GetMapping("hello-api")
    @ResponseBody
    public Hello helloApi(@RequestParam("name") String name) {
        Hello hello = new Hello();
        hello.setName(name);
        return hello;
    }

    static class Hello {
        private String name;

        public String getName() {
            return name;
        }

        public void setName(String name) {
            this.name = name;
        }
    }
```
- 실행

- key와 value로 결과가 반환됨