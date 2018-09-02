## enum(Enumeration)
1. 열거형 선언하기

```java
public enum exam {

  Exam1,
  Exam2,
  Exam3
}
```
 -열거형으로 선언된 순서에 따라 0부터 인덱스 값을 가진다.  
 -순차적으로 증가된다.
 2. enum 메소드
* valueOf(String arg) : String값을 enum에서 가져옴. 값이 없으면 예외 발생
* valueOf(Class<T> class, String arg) : 넘겨받은 class에서 String을 찾아, enum에 가져옴. valueOf(String arg)는 내부적으로 자기자신 Class를 가져옴.
* values() : enum의 요소들을 순서대로 enum타입의 배열로 리턴.
* name(): 호출된 값의 이름을 String 으로 리턴.
* ordinal() : 해당값이 enum에 정의된 순서를 리턴.
* compareTo(E o) : enum과 지정된 객체의 순서를 비교
     * 지정된 객체보다 작은경우 음의정수 리턴
     * 지정된 객체와 같으면 0 리턴
     * 지정된 객체보다 큰 경우 양의정수 리턴
* equals(Object other) : 지정된 객체가 enum 정수와 같은 경우, true 를 리턴.

## @Override

- 상속받은 클래스에서 메소드를 바꿀 필요가 있을 때 재정의 하는 것

## Map

- 키값(key)과 값(value)가 쌍으로 존재하는 형식

```java

public static void main(String[] args){
  Map<String, String> examMap = new HashMap<String, String>();

  examMap.put("1번", "1번쨰값");
  examMap.put("2번", "2번째값");
  examMap.put("3번", "3번쨰값");

  for(int i = 1; i<= testMap.size(); i++){
    System.out.print(examMap.get((i+"번")));
  }
}
```
이런식으로 값을 넣어준다면 1번부터 3번까지의 값이 모두 Map 한곳에 담겨있다가 꺼내서 사용할 수 있다. 따라서 위 코드의 출력은
1번째값
2번째값
3번쨰값
이 될 것이다.
