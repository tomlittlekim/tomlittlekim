# JPA에서 키워드 By의 역할

![image](https://github.com/tomlittlekim/tomlittlekim/assets/43326452/9e1321bb-a51f-4557-a75c-81953f3f9b97)

위는 JPA 공식 문서의 특정 부분인데, 첫 번째 키워드 By는 실제 기준 서술어의 구분 기호 역할을 한다고 쓰여있다.

ID 역순 정렬로 모두 불러오는 쿼리를 만들 때, 상식적으로 findAllOrderByIdDesc(); 가 말이 되지만, 이건 오류를 발생시킨다. findAllByOrderByIdDesc();로 변경하면 잘 동작하는데, 서술어와 제한 쿼리를 구분을 지어야 했기 때문인가보다.
