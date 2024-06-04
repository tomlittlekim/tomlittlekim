# JUnit Test 한 번에 여러 테스트 진행하기

코딩 감각을 되살릴겸 코딩테스트를 0단계부터 다시 해보고 있다.

이번에는 개발툴로 문제를 실행&정리하고 있었는데, 문제의 여러 입출력을 바꿔가며 결과를 테스트하는 게 무식한 방법이라는 생각이 들었고, 분명 다른 방법이 있을 거라고 생각해서 알아봤다.

 

@ParameterizedTest 어노테이션과 @CsvSource 어노테이션을 활용한 방법이다.

이 외에도 @ValueSource, @MethodSource가 있지만 내가 필요한 것은 간단하게 여러 개의 파라미터를 입력하는 것이기 때문에 @CsvSource를 이용했다. 이름에서 유추할 수 있듯이 csv형태로 구성해야 한다.  

```
@ParameterizedTest  
@CsvSource({"98,2,1", "34,3,0"})  
void exam_5(int num, int n, int expected) {  
    System.out.printf("num:%d\nn:%d\nexpected:%d\n\n", num, n, expected);  
    Assertions.assertEquals(expected, main.exam_5(num, n));  
}
```
![image](https://github.com/tomlittlekim/tomlittlekim/assets/43326452/6d8cebf6-a5a7-4371-8391-f032a01033e7)
참조: (https://stackoverflow.com/questions/61483452/parameterized-test-with-two-arguments-in-junit-5-jupiter)  

- 추가 -  
배열 파라미터로 테스트가 필요하다면 (리스트도 가능, Arrays.asList(...);)
```
@ParameterizedTest
@MethodSource("exam11Data")
void exam_11(int a, int d, boolean[] included, int expected) {
    Assertions.assertEquals(expected, LEVEL_0.exam_11(a, d, included));
}

static Stream<Arguments> exam11Data() {
    return Stream.of(
            Arguments.of(3, 4, new boolean[]{true, false, false, true, true}, 37)
            , Arguments.of(7, 1, new boolean[]{false, false, false, true, false, false, false}, 10)
    );
}
```
