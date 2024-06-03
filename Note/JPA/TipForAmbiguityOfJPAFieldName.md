# JPA 필드명의 모호성 해결

![image](https://github.com/tomlittlekim/tomlittlekim/assets/43326452/f46ff838-2057-4add-9db2-1e9a8f684611)

 Person이라는 클래스가 ZipCode가 있는 Address를 필드로 가지고 있다고 가정했을 때, findByAddressZipCode(Zipcode zipcode);라는 메소드를 만드는 경우가 있을 수 있다.

 JPA는 AddressZipCode를 하나의 필드로 해석하고 도메인 클래스에서 해당 필드를 찾을 것이다. 찾으면 해당 필드를 사용해서 진행하고, 못 찾으면 낙타표기법에 기준하여 분할을 시도한다. 
처음에는 AddressZip과 Code로 나눌 것이다. 그래도 못 찾으면 기준점을 왼쪽으로 옮겨가며 찾기 시작한다. 그 다음은 Address와 ZipCode가 될 것이다. 
이렇게 우리 의도대로 정확하게 찾을 수도 있지만, 애매모호한 경우가 있을 수 있다.

 만약 Person 클래스에 addressZip이라는 필드가 있다면 어떨까?
첫 번째 분할에서 addressZip 필드를 찾았고 그대로 빌드를 진행할 것이다. 
남은 code라는 필드가 없으면 빌드에 실패할 것이고 있으면 빌드는 성공하겠지만 의도한 바와 다른 결과를 가져올 것이다.


 이를 해결하기 위해 어찌해야할까?
밑줄을 사용하여 해결하면 된다. 
메소드 명을 findByAddress_ZipCode(ZipCode zipCode); 
이렇게 만들면 모호성이 해결되어 올바른 결과를 가져온다.


 하지만 밑줄은 예약어로 취급되기 때문에, Java 네이밍 규칙(낙타표기법)을 사용할 것을 강력하게 권장하고 있기는 하다.
