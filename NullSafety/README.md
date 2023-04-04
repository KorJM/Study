# NULL SAFETY
### null safety란?
null 값을 가지는 변수와 객체를 명시적으로 지정하여 null 값을 안전하게 처리하기 위한 기능<br>
<li>대표적으로 NullPointerException을 방지하기위한 기능</li><br>

### NullPointerException이란?
변수를 통해 객체의 메소드나 프로퍼티를 호출하는 등의 작업을 할 떄, 해당 변수가 null 값을 가지고 있으면 발생하는 에러 <br>

<img width="557" alt="image" src="https://user-images.githubusercontent.com/114234223/229758090-88144ee0-5221-407d-9c17-34fbe7f096bb.png">

<img width="737" alt="image" src="https://user-images.githubusercontent.com/114234223/229758425-f50f382a-ce48-4882-9e07-274d0f1889b3.png">

null safety기능이 적용되지 않은 Java를 사용하여 name 변수 값의 길이를 출력하는 코드인데 <br>
name의 값이 null이므로 String.length()메소드를 호출 할 수 없어  NullPointerException이 발생한 상황입니다<br><br>
여기서 중요한 것은<br>
<strong>complie 단계에선 오류가 발생하지 않았지만 run time에서 null값을 참조하려는 코드가 실행될 때 오류가 발생 한 것입니다.</strong><br><br>

이런 문제를 해결하기 위해 null safety가 도입되었고 그 목적은 <br>
<strong>null 값이 발생할 가능성이 있는 변수나 객체를 사용할 때 개발자의 실수로 인해 <br>run time에서 발생할 오류를 complie 단계에서 잡아내는 것</strong><br><hr>
  
## null safety에서 제공하는 몇가지 연산자와 키워드
### null safety를 제공하는 언어
  <li>Kotlin</li>
  <li>C# 8.0</li>
  <li>Swift 1.2</li>
  <li>Dart 2.12 등등</li>
<br> Dart를 사용하여 몇가지 연산자와 키워드를 알아보겠습니다.<br>

### <li>?</li>

<img width="526" alt="image" src="https://user-images.githubusercontent.com/114234223/229762164-e709023e-37eb-4ef2-953c-b4df5a9fffcc.png">

코드를 보시면 전 페이지의 자바 코드와 동일한 작업을 하는 코드입니다.<br>
하지만 dart는 null safety가 적용된 언어이기에 실행하기 전부터 <br>
name 변수가 null값을 가질 수 없다고 오류 메시지를 보내줍니다.

<img width="87" alt="스크린샷 2023-04-04 오후 7 21 52" src="https://user-images.githubusercontent.com/114234223/229763064-687069fd-0f37-42d9-9e3a-7fa5cf310494.png">

기본적으로 dart에서는 이런식으로 변수 선언을 하고 초기화를 하면 <br>
null 값을 가질 수 없는 non-nullable 변수로 생성됩니다.

<img width="348" alt="스크린샷 2023-04-04 오후 7 22 05" src="https://user-images.githubusercontent.com/114234223/229763273-d61dfef5-c82b-47c5-8aca-49ae48ddc496.png">

해당 오류를 고치는 법은 당연히 null 값이 아닌 문자열을 할당 시켜주거나 또는 타입뒤에 ?를 붙여주는 것입니다. <br>
?는 null safety 기능에서 사용하는 연산자로 해당 변수 또는 프로퍼티가 null 값을 가질 수 있는지를 표현해줍니다.<br>

<img width="528" alt="image" src="https://user-images.githubusercontent.com/114234223/229765885-5adf3f1e-7ef3-4850-b45a-0109e00c1f79.png">

이런식으로 변수선언 해주면 name변수가 null값을 가질 수 있는 nullable 변수로 선언됩니다.<hr>

### <li>?.</li>
그런데 다른 오류가 생기게 됩니다.<br>

<img width="348" alt="스크린샷 2023-04-04 오후 7 35 19" src="https://user-images.githubusercontent.com/114234223/229766135-8606d4fa-a5e8-499f-93b6-7aeb23e725ae.png">

메시지를 보시면 '수신자가 null 일 수 있으므로 length 프로퍼티를 무조건적으로 액세스 할 수 없다.' 라고 뜹니다. <br>
저희가 name 변수를 nullable변수로 선언했기 때문에 name의 값이 null일 경우에 프린트 문장에서<br>
nullpointerexception이 발생할 수 있으므로 컴파일러가 미리 에러 메시지를 보내주는 것입니다. <br><br>
<strong>이런식으로 잘못된 null값 참조를 프로그램이 실행되기 전에 컴파일러가 체크해주는것이 <br>null safety의 목적이자 존재 이유입니다.</strong> <br>해결 방법을 보시면 엑세스방법을 조건부로 만들어라 라고 말해줍니다.

<img width="528" alt="image" src="https://user-images.githubusercontent.com/114234223/229766870-d910af8a-1ebc-4a00-a014-3c7c724a05c3.png">

그 방법으로 ?. 연산자를 사용하여 nullable 변수를 사용할 때 그 값에 따라 출력 결과를 바꿔주는 <br>
조건부 달아주어 안전하게 호출하는 것입니다. <br>
name의 값이 null이 아닐때만 length속성에 접근하여 값을 출력하고 null일 경우에는 null값을 가져옵니다.<br>
<hr>

### <li>required</li>

<img width="524" alt="image" src="https://user-images.githubusercontent.com/114234223/229769637-9a269dbf-9812-4138-8e62-007d218c78fe.png">

코드를 보시면 add 메소드의 파마미터 a와 b에 에러가 발생했는데 에러 내용을 보시면 <br>
해당 파라미터는 non-nullable이기 때문에 null값을 가질 수 없지만 <br>
현재 암묵적인 기본값은 null이므로 에러가 발생한 것입니다.

<img width="325" alt="스크린샷 2023-04-04 오후 7 51 15" src="https://user-images.githubusercontent.com/114234223/229769890-e3601161-a647-4986-9ad6-901b7f570eb5.png">

해결법으로 명시적으로 null이 아닌 defalut value를 지정 해주거나 <br>
‘required’ 라는 수식어를 추가해보세요 라고 나옵니다.

<img width="524" alt="image" src="https://user-images.githubusercontent.com/114234223/229770030-e6f59f97-8d15-4c8d-8232-2c86d8f59bdb.png">

이런식으로 required라는 수식어를 추가해주면 매개변수나 필드가 반드시 초기화 되어야 한다는 의미가 생기고 <br>
위와 같이 함수 호출 시 반드시 값을 할당 해주어야 하며 null 값은 허용되지 않습니다. 
<br><hr>

## null safety의 장점
<li>
  프로그램의 안정성 향상
</li>
<li>
  디버깅 시간 절약 <ul>null safety를 적용하면 null 값을 사용할 때 발생할 수 있는 오류들을<br>
                   컴파일러가 미리 체크해줘서 실행되는 도중에 예기치 않은 오류가 발생할 확률이 줄어들어 프로그램의 안정성이                    향상되고,<br>
                   run time시 발생하는 에러를 줄이고 컴파일 단게에서 수정이 가능하므로 디버깅 시간 또한 절약됩니다.
                </ul>
</li>
<li>
  코드 가독성 향상
</li>
<li>
  코드 유지보수 용이성 향상<ul>null safety를 적용하면 변수가 null값을 참조할 수 있는지 아닌지 명시적으로 표시하며 <br>
                         또한 잘못된 null값 참조를 방지하기 위한 예외 처리 코드를 별도로 작성할 필요가 없기때문에 <br>
                         코드가 간결해지고 가독성이 향상며 이는 코드를 이해하는데 도움이 되어 유지보수에도 유리해집니다.                        </ul>
</li>
