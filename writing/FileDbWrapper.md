#### FileDbWrapper

1. 생성자

```java
public FileDbWrapper(String folderName, String fileName){
  this(folderName,  fileName, DEFAULT_DELIMETER);
}
public FileDbWrapper(String folderName, String fileName, String delimiter)  {
  this.delimiter = delimeter;
  this.fileName = fileName;
  this.File = ResourceUtil.getFile("filedb", folderName, fileName);
}
```

  - 입력받은 folderName, fileName 을 지정
  - ReSourceUtil을 통해 지정된 폴더의 경로를 얻어와서 경로에 파일이 있으면 그 파일을 반환, 없으면 새로 생성하여 반환 받음.


2. 메소드

```java
public boolean hasValueOf(String key, String value, String line) {
  //
  Integer keyIndex = this.keyIndexMap.get(key);

  if (keyIndex == null) {
    return false;
  }

  StringTokenizer tokenizer = new StringTokenizer(line, delimiter);

  for (int i = 0; i < keyIndex; i++) {
    tokenizer.nextToken();
  }

  String token = tokenizer.nextToken();
  if (value.equals(token)) {
    return true;
  } else {
    return false;
  }
}
```

- 입력된 key값으로 해당 line에 value 값과 같은 데이터가 있는지 확인함.
- StringTokenizer 를 사용하여 line에 delimiter로 구분되어있는 데이터들을 nextToken 메소드로 읽어온다.

```java
public Object convertTo(String readLine, Class<?> clazz) {
		//
		StringTokenizer tokenizer = new StringTokenizer(readLine, getDelimiter());
		int tokenCount = this.keyIndexMap.size();

		for (int i = 0; i < tokenCount; i++) {
			tokenizer.nextToken();
		}

		String json = tokenizer.nextToken();
		return ((new Gson()).fromJson(json, clazz));
	}
```
- 읽어온 데이터(readLine) 을 해당 객체(clazz)로 바꿔주는 메소드이다.
- StringTokenizer를 통하여 delimietr로 구분된 데이터를 읽어오고, 그 값을 json형태로 변환한다.
- json으로 받은 값을 통해 clazz에 해당하는 객체로 변환해준다.

```java
public String convertFrom(Object object) {
		//
		StringBuilder builder = new StringBuilder();
		Iterator<String> keyIter = this.keyIndexMap.keySet().iterator();
		while (keyIter.hasNext()) {
			String keyName = keyIter.next();
			builder.append(callGetMethod(object, keyName)).append(getDelimiter());
		}

		builder.append((new Gson()).toJson(object));

		return builder.toString();
	}
```

- 입력받은 객체의 데이터들을 Iterator를 통하여 꺼낸다.
- Stringbuilder 로 꺼낸 데이터들을 DEFAULT_DELIMETER 로 구분하여 조합한다.
- 조합된 데이터를 String타입으로 변환하여 반환한다.

```java
private String callGetMethod(Object object, String attrName) {
		//
		String result = null;
		try {
			String methodName = "get" + attrName.substring(0, 1).toUpperCase() + attrName.substring(1);
			Method getMethod = object.getClass().getMethod(methodName);
			result = (String) getMethod.invoke(object);
		} catch (IllegalAccessException e) {
			e.printStackTrace();
		} catch (IllegalArgumentException e) {
			e.printStackTrace();
		} catch (InvocationTargetException e) {
			e.printStackTrace();
		} catch (NoSuchMethodException e) {
			e.printStackTrace();
		} catch (SecurityException e) {
			e.printStackTrace();
		}

		return result;
	}
```
- attrName.substring(0, 1) :subString 메소드로 attrName의 0번째에서 1번째 문자를 받아옴.
- toUpperCase() : 대문자로 변환
- attrName.substring(1) : attrName 의 1번째 문자부터 읽어옴
- 위의 3가지를 조합하여 methodName을 만든다.
```java
Method getMethod = object.getClass().getMethod(methodName);
```
해당 객체(object) 의 methodName을 가진 메소드를 불러옴
