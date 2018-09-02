### ArrayList(String)

#### ArrayList의 저장공간에 대하여.

##### add() 함수

1. 배열의 크기는 늘리거나 줄일 수 없다.(1)
2. ArrayList 의 remove와 add에서 사용되는 배열도 마찬가지.(2)
3. ArrayList에서 사용된 배열의 크기보다 많은 데이터를 넣으려면 배열의 크기를 키워야 하고, 그러기 위해서는 temp배열(size = 배열.length+1)을 하나 만들어서 기존의 배열의 데이터를 temp배열에 저장한 후 반환해주어야 함.

--> 배열의 크기보다 많은 데이터를 넣으려면 add할 때 마다 배열의 모든 요소를 복사(for문 사용)해야하는 상황이 발생함.

##### remove() 함수
1. 1, 2 마찬가지
3. (두가지 방법으로 생각해봄)
  - 저장공간 의 효율성(?)(맨처음 구현한 방법)
    - remove함수를 사용하여 요소를 삭제한 경우 삭제된 index의 비어있는 공간을 맨 뒤로 밀어낸 후 배열의 크기를 줄여서 저장공간을 확보.

  ```java

    	public void remove(int index) {
    		//
    		String[] tempArray = new String[array.length];

    		tempArray = copyOf(array, index);
    		for (int i = index; i < size - 1; i++) {  
    			tempArray[i] = array[i + 1];
    		}
    		array = tempArray;

        tempArray = arraySizeDecrease(tempArray);

    		size--;
    	}
  ```
    *arraySizeDecrease(tempArray)는 배열의 크기를 하나 줄이는 함수. for문을 사용해서 배열을 복사한 후 반환

  - 함수의 효율성(?)
    - 위의 방법처럼 배열의 크기를 줄여서 저장공간을 확보하는 경우 배열의 크기는 조절할 수 없으므로 크기가 하나 작은 배열을 만들어 반환해야 하는데, 이 과정에서 사용되는 함수들의 효율성이 떨어진다고 생각됨. (다시 List에 값을 추가할 때에도 비어있는 공간이 없으므로 복사하여 반환한 배열에 추가해야함.)
    - 그래서 remove함수를 사용한 후 삭제된 index의 비어있는 공간을 맨뒤로 밀어낸 후 배열의 크기를 줄여주지 않고 그대로 둔다.

    ```java

    public void remove(int index) {
    		//
    		String[] tempArray = new String[array.length];

    		tempArray = copyOf(array, index);
    		for (int i = index; i < size - 1; i++) {

    			tempArray[i] = array[i + 1];

    		}
    		array = tempArray;
    		size--;
    	}

    ```
    * 이경우 비어있는 공간이 많아질 수 있다고 생각,

  ->두가지 방법의 병합.
    - 비어있는 공간의 크기가 일정크기 이상이 되면 배열의 크기를 줄인다.

    ```java
    public void remove(int index) {
    		//
    		String[] tempArray = new String[array.length];

    		tempArray = copyOf(array, index);
    		for (int i = index; i < size - 1; i++) {

    			tempArray[i] = array[i + 1];

    		}
    		array = tempArray;
    		size--;

    		if (array.length - size > 50) {

    			array = arraySizeDecrease(array, 40);
    		}
    	}
    ```
    *arraySizeDecrease(array, 40) 함수는 위의 if문에서 빈공간이 50이상 생길 경우 배열의 크기를 40만큼 줄여서 저장공간을 확보할 수 있도록 함.





###### 참고자료 :
http://apphappy.tistory.com/81,
http://www.nextree.co.kr/p6506/
