# Java - ArrayList 1, 2차원 배열 선언

#### 1차원 배열

> 바로 인스턴스를 생성해줍니다.

```java
ArrayList<자료형> 변수명 = new ArrayList<자료형>();
```



#### 2차원 배열

> 인스턴스 생성 시 배열 부호[] 를 사용합니다.
>
> 각각의 배열[index]를 ArrayList로 선언해줍니다.

```java
ArrayList<Integer>[] list = new ArrayList[n];
for (int i = 0; i < n; i++) {
    list[i] = new ArrayList<Integer>();
} 
```

- **이렇게 하면, n개의 ArrayList<Integer> 객체를 생성하고, 배열에 저장할 수 있습니다. 각 ArrayList는 Integer 값들을 저장할 수 있으며, 각각의 ArrayList는 서로 다른 크기를 가질 수 있습니다.**

```java
// 값을 넣는 방법
// [index]번 인덱스에 Value 값 추가
list[0].add(1);
list[0].add(2);
list[1].add(3);

// 출력
for(int num : list[n]){
    System.out.println(num); // list[n]에 있는 모든 값 출력
}

// 2중 for문
for (int i = 0; i < n; i++){
    for (int j = 0; j < arr[i].size(); j++){ // 이 부분을 forEach문으로 대체 할 수 있음
        System.out.println(arr[i].get(j));
    }
}
```

