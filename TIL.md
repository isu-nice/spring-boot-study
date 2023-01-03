# 테스트 코드 작성
- public class로 관리하지 않아도 됨
- for each

우테코 프리코스를 진행하면서 `IllegalArgumentException` 을 정말 많이 사용했던 경험이 있다.   
후에는 습관적으로 IllegalArgumentException을 사용했던 것 같다.   
그런데 이번에 스프링 강의를 들으면서 `IllegalStateException` 을 접하게 되었고, 두 예외 처리의 차이점이 무엇인지 궁금해졌다.

### IllegalArgumentException
- 잘못된 인수를 가진 호출을 받았을 때 사용
- 예시 (사용자의 입력이 형식에 어긋난 경우의 예외처리)
```java
    private void validatePrice() {
        if (price > MINIMUM_PRICE) {
            throw new IllegalArgumentException("최소 금액은 100원 이상이어야 합니다.");
        }
```

### IllegalStateException
- 호출받은 객체가 요청을 수행하기에 적합하지 않은 상태일 때 사용
- 예시 (중복된 이름이 존재하는 경우의 예외처리)
```java
    private void validateDuplicateMember(Member member) {
        memberRepository.findByName(member.getName())
                .ifPresent(member1 -> {
                    throw new IllegalStateException("이미 존재하는 회원입니다.");
                });
    }
```