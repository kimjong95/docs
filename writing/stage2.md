### Java Collection Framework(JCF)
 : Java에서 데이터를 저장하는 기본적인 자료구조들을 한 곳에 모아 관리하고 편하게 사용하기 위해서  제공하는 것을 의미한다.
 ![JCF](./C:/Users/김종현/Pictures/JCF.jpg)

 #### Collection Interface : 모든 콜렉선의 상위 인터페이스로써 콜렉션들이 갖고 있는 핵심 메소드를 선언
 1. List Interface : Collection 인터패이스를 확장한 자료형으로 요소들의 순서를 저장하여 특정위치에 요소에 삽입하거나  접근하 할 수 있다.
  - ArrayList : 빠르고 크기를 마음대로 조정할 수 있는 배열, 단방향 포인터 구조로 순차적인 접근에 강점이 있다.
  - Vector : ArrayList의 구버전으로 모든 메소드가 동기화되어 있다.
  - LinkedList :  양방향 포인터구조로 데이터 삽입, 삭제가 빈번할 경우 유용하다.
 2. Set Interface : 집합을 정의하며 요소의 중복을 허용하지 않는다.
  - Hash Set : 접근속도가 가장빠르며 순서를 예측할 수 없다.
  - LinkedHash SEt : 추가된 순서 또는 가장 최근에 접근한 순서대로 접근 가능

#### Map Interface : Key 와 Value의 쌍으로 연관지어 저장하는 객체

1. HashMap : Map 인터페이스를 구현하기 위해 해시테이블을 사용한 클래스이며 중복을 허용하지 않고 순서를 보장하지 않음. key 와 값으로 null이 허용됨.
2. HashTable : HashMap보다는 느리지만 동기화가 지원된다. key와 값으로 null이 인정되지 않음
3. LinkedHashMap : 기본적으로 HashMap을 상속받아 유사하다. Map에 있는 엔트리들의 연결리스트가 유지되므로 입력한 순서대로 반복이 가능하다.


#### Collection 의 메소드

메소드명        |  설명
-------------- | ---------
**int size ()** | 이 콜렉션의 요소 수를 리턴합니다. 이 콜렉션에 Integer.MAX_VALUE 보다 많은 요소 가 포함되는 경우 는 Integer.MAX_VALUE를 돌려줍니다 .
**boolean isEmpty ()** | 반환 사실 이 컬렉션에 요소가없는 경우 true
**Iterator < E > 반복자 ()** | 이 컬렉션의 요소의 반복자를 돌려줍니다. 요소가 돌려 주어지는 순서에 관한 보증은 없습니다 (이 컬렉션이 보증을 제공하는 클래스의 인스턴스가 아닌 경우).
**boolean remove ( Object  o)** | 지정된 요소의 단일의 인스턴스를이 콜렉션으로부터 삭제합니다 (옵션의 오퍼레이션). 이 콜렉션에 그러한 요소가 1 개 이상있는 경우는, (e == null : e.equals (e)) 와 같은 요소 e를 삭제합니다 . 반환 사실 (이 호출의 결과, 컬렉션이 변경되었을 경우, 동등 또는) 지정된 요소가이 컬렉션에 포함 된 경우.
** booelan addAll ( Collection <? extends E > c)** | 지정된 컬렉션의 모든 요소를이 컬렉션에 추가합니다 (임의의 오퍼레이션). 작업이 진행되는 동안 지정된 컬렉션이 수정되면이 작업의 동작은 정의되지 않습니다. 지정된 콜렉션이이 콜렉션이며이 콜렉션이 비어 있지 않으면이 호출의 동작은 정의되지 않습니다.
**boolean equals ( Object  o)** | 지정된 객체와이 컬렉션이 동일한 지 어떤지를 비교합니다.

■ 출처

http://withwani.tistory.com/150
http://blog.naver.com/windziel/60048694876
http://www.gliderwiki.org/wiki/99
http://www.java-school.net/java/10.php


출처: http://hackersstudy.tistory.com/26 [공대인들이 직접쓰는 컴퓨터공부방]
### Iterator


Iterator 란?



Iterator는 자바의 컬렉션 프레임웍에서 컬렉션에 저장되어 있는 요소들을 읽어오는 방법을 표중화 하였는데 그 중 하나가 Iterator이다.

``` Java
public interface Iterator {

boolean hasNext();

Object next();

void remove();

}
```
메소드명 | 설명
--------|------
booelan hasNext() | 읽어올 요소가 남아있는지 확인하는 메소드로써 있으면 true, 없으면 false를 반환한다.
Object next() | 읽어올 요소가 남아있는지 확인하는 메소드이다 있으면 true, 없으면 false를 반환한다.
void remove() | next()로 읽어온 요소를 삭제한다. next()를 호출한 다음에 remove()를 호추래야 한다.



출처: http://vaert.tistory.com/108 [Vaert Street]
