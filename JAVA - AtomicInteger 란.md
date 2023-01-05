## JAVA - AtomicInteger 란 ?

> `AtomicInteger`는 `int` 자료형을 갖고 있는 `wrapping` 클래스 입니다.
>
> `wrapper class` 는 기본 자료타입을 객체로 다루기 위해서 사용하는 클래스들입니다.
>
> `AtomicInteger`는 `멀티쓰레드` 환경에서 동기화 문제를 별도의 `synchronized` 키워드 없이 해결하기 위해서 고안된 방법입니다.
>
> ###### 일반적으로 동기화 문제는 **synchronized, Atomic, volatile** 세가지 키워드로 해결한다.



#### 객체 생성

`AtomicInteger`는 다음과 같이 생성이 가능하며, 초기값은 `0`, 초기값을 변경하고 싶으면 인자로 `int` 변수로 전달하면 됩니다.

![image-20230105200051519](C:\Users\sbpar\AppData\Roaming\Typora\typora-user-images\image-20230105200051519.png)     

##### 결과

![image-20230105200122315](C:\Users\sbpar\AppData\Roaming\Typora\typora-user-images\image-20230105200122315.png) 



#### get(), set(), getAndSet()

`AtomicInteger`의 `int` 값을 변경하려면 `set(int)`, 값을 읽으려면 `get()`을 사용해야 합니다.

![image-20230105200217755](C:\Users\sbpar\AppData\Roaming\Typora\typora-user-images\image-20230105200217755.png) 

##### 결과

![image-20230105200231023](C:\Users\sbpar\AppData\Roaming\Typora\typora-user-images\image-20230105200231023.png) 

`getAndSet(int)`은 현재의 `value`를 `return`, 인자로 전달된 값으로 업데이트합니다.

![image-20230105200324041](C:\Users\sbpar\AppData\Roaming\Typora\typora-user-images\image-20230105200324041.png) 

##### 결과

![image-20230105200329591](C:\Users\sbpar\AppData\Roaming\Typora\typora-user-images\image-20230105200329591.png) 

#### compareAntSet()

`compareAndSet(expect, update)`는 현재 값이 예상하는 값(expect)과 동일하다면 update 값으로 변경해주고 `true`를 리턴해 줍니다. 그렇지 않다면 데이터 변경은 없고 `false`를 리턴합니다.

![image-20230105200508094](C:\Users\sbpar\AppData\Roaming\Typora\typora-user-images\image-20230105200508094.png) 

![image-20230105200514830](C:\Users\sbpar\AppData\Roaming\Typora\typora-user-images\image-20230105200514830.png) 

#####  결과

![image-20230105200523988](C:\Users\sbpar\AppData\Roaming\Typora\typora-user-images\image-20230105200523988.png) 



#### addAndGet() etc..

`getAndIncrement()` 현재 값 리턴하고 +1 증가

`incrementAndGet()` +1 증가시키고 변경된 값 리턴

`getAndDecrement()` 현재 값 리턴하고 -1 감소

`decrementAndGet()` -1 감소시키고 변경된 값 리턴

`getAndAdd(newValue)` 현재 값 리턴하고, 현재 값에 `newValue`를 더하기

`addAndGet(newValue)` 현재 값에 `newValue`를 더하고, 그 결과를 리턴

`addAndGet()`은 현재 값에 `newValue`를 더하고, 그 결과를 리턴

##### ![image-20230105202114448](C:\Users\sbpar\AppData\Roaming\Typora\typora-user-images\image-20230105202114448.png) 

##### 결과

![image-20230105202133020](C:\Users\sbpar\AppData\Roaming\Typora\typora-user-images\image-20230105202133020.png) 

