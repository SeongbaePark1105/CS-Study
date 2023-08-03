# [Java] StringBuilder 메소드



```
코딩 테스트 문제를 풀면서 문자열을 더하여 문자를 이를 떄에는 StringBuilder를 사용하는 게 좋다고 합니다.

그래서 기본 메소드들과 코딩 테스트때 사용한 메소드들을 정리해보았습니다.
```



#### [ String 클래스와 동일 메소드 ]

##### `charAt()`

- 특정 인덱스 위치의 문자 반환

##### `indexOf() / lastIndexOf() `

-  문자열 검색해서 위치 반환

##### `length() `

- 문자열 길이 반환

##### `replace()` 

-  검색된 문자열 교체

##### `substring()`

- 특정 인덱스 범위 내 문자열을 복사해서 새로 생성된 인스턴스 반환

##### `toString()`

- 문자열 출력



#### [ append() ]

- 문자열을 추가합니다.

```java
StringBuilder sb = new StringBuilder("Hello");
sb.append(" World");
System.out.println(sb); // "Hello World"
```

------



#### [ capacity() ]

- `String` 클래스와 다르게 `char[]`배열 사이즈를 여유 있게 확보합니다.
- 현재 `char[]`배열이 가진 사지으 정보를 반환합니다.
- `length()`는 실제 데이터가 들어있는 문자열 자체의 길이이고 `capacity()`는 현재 배열 사이즈 입니다.
- `append()` 등 문자열 조정할 때 배열 사이즈가 자동으로 변경됩니다.

```java
StringBuilder sb = new StringBuilder("Hello");
		
System.out.println(sb.length());	// 5
System.out.println(sb.capacity()); 	// 21
		
sb.append(" World");
System.out.println(sb);             // "Hello World"
		
System.out.println(sb.length()); 	// 11
System.out.println(sb.capacity()); 	// 21
		
sb.append(" Hi everybody!!!!");
System.out.println(sb);             // Hello World Hi everybody!!!!

System.out.println(sb.length()); 	// 28
System.out.println(sb.capacity()); 	// 44
```



------



#### [ delete() ]

- `매개변수`로 전달받은 `인덱스` 사이의 문자열을 제거합니다.
- `매개변수` : 인덱스 시작점, 인덱스 끝점 + 1
- 문자열에서 시작과 끝은 항상 `시작 <= 범위 < 끝` 형태입니다.

```java
StringBuilder sb = new StringBuilder("Hello");
sb.append(" World");
System.out.println(sb); // "Hello World"

sb.delete(6, 9); 		// 인덱스 값 6 ~ 8 삭제
System.out.println(sb); // "hello ld"
```



------



#### [ deleteCharAt() ]

- 특정 인덱스의 한 문자만 삭제합니다.
- `delete()` 메소드에서 범위를 한 글자만 잡는 것과 동일한 효과를 가집니다.

```java
StringBuilder sb = new StringBuilder("Hello");

sb.append(" World");
System.out.println(sb); // "Hello World"
		
// a.delete(6,7) 과 같음
a.deleteCharAt(sb);
System.out.println(sb);	// "Hello orld"
```



------



#### [ insert() ]

- 특정 위치에 문자열을 삽입합니다.
- `매개변수`로 받은 인덱스 위치부터 `문자열`을 삽입합니다.
  - 여기서 중요한 것은 `문자열`입니다.

```java
StringBuilder sb = new StringBuilder("He World");
		
sb.insert(2, "llo");
System.out.println(sb);	// "Hello World"
		
sb.insert(5, !!);
System.out.println(sb); // "Hello!! World"
```



------



#### [ setCharAt() ]

- 특정 위치에 문자의 값을 변경합니다.
- `매개변수`로 받은 인덱스 위치에 있는 문자를 `매개변수`로 받은 문자의 값으로 바꿉니다.

```java
StringBuilder sb = new StringBuilder("Hello World");

sb.setCharAt(0, 'h');
System.out.println(sb); // "hello World"

sb.setCharAt(5, '-');
System.out.println(sb); // "hello-World"
```

