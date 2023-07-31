# Fibonacci 3가지 차이- Recursion,DP, Iteration / 시간 복잡도, 공간 복잡도 차이

태그: 알고리즘

**📌✔**

## #Fibonacci 연산 - recursion

```cpp
int Fibo(int num)
{

   if(num == 1)
      return 1;
   else if( num ==2 )
      return 1;
   else
      return Fibo(num-1)+Fibo(num-2);

}
```

![스크린샷 2023-07-29 오후 11.03.09.png](Fibonacci%203%E1%84%80%E1%85%A1%E1%84%8C%E1%85%B5%20%E1%84%8E%E1%85%A1%E1%84%8B%E1%85%B5-%20Recursion,DP,%20Iteration%20%E1%84%89%E1%85%B5%E1%84%80%E1%85%A1%20b0665d8b27ad4d509606330d26b67436/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-07-29_%25E1%2584%258B%25E1%2585%25A9%25E1%2584%2592%25E1%2585%25AE_11.03.09.png)

### 시간 복잡도 : O(2^n)

- 연속 함수 호출로 인한 stack overflow 문제 발생 가능성 높음

## #Fibonacci 연산 - DP (Memoization)

```cpp
int Fibo(int num) {
	if(memo[num]) {
		return memo[num];
	} else {
		if(num<2) return n;
		memo[num]=Fibo(num-1)+Fibo(num-2);
		return memo[num];
	}
}
```

![스크린샷 2023-07-29 오후 11.06.40.png](Fibonacci%203%E1%84%80%E1%85%A1%E1%84%8C%E1%85%B5%20%E1%84%8E%E1%85%A1%E1%84%8B%E1%85%B5-%20Recursion,DP,%20Iteration%20%E1%84%89%E1%85%B5%E1%84%80%E1%85%A1%20b0665d8b27ad4d509606330d26b67436/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-07-29_%25E1%2584%258B%25E1%2585%25A9%25E1%2584%2592%25E1%2585%25AE_11.06.40.png)

### 시간 복잡도 : O(n)

- 연속 함수 호출로 인한 stack overflow 문제 발생 가능성 높음
- 메모이제이션을 통해 동일한 계산이 반복되는 것을 방지
- 계산된 값을 저장할 테이블 존재

## #Fibonacci 연산 - iteration (Bottom-Up Approach)

```cpp
int Fibo(int num) {

	int memo[3];
	memo[0]=0;
	memo[1]=1;
    
	for (int i=2; i<=num;i++) {
		memo[i]=memo[i-1]+memo[i-2];
	}
    
	return memo[num];
}

//메모리를 더 아끼는 법

int Fibo(int num) {

	int memo[3];
	memo[0]=0;
	memo[1]=1;
    
	for (int i=2; i<=num;i++) {
		memo[i%3]=memo[(i-1)%3]+memo[(i-2)%3];
	}
    
	return memo[num];
}
```

### 시간 복잡도 : O(n)

- 메모이제이션을 통해 동일한 계산이 반복되는 것을 방지
- 계산된 값을 저장할 테이블 존재

🔗[https://itfordoit.tistory.com/85](https://itfordoit.tistory.com/85) 

🔗[https://junghyun100.github.io/Fibonacci을구현방법-차이점은(시간복잡도등)/](https://junghyun100.github.io/Fibonacci%EC%9D%84%EA%B5%AC%ED%98%84%EB%B0%A9%EB%B2%95-%EC%B0%A8%EC%9D%B4%EC%A0%90%EC%9D%80(%EC%8B%9C%EA%B0%84%EB%B3%B5%EC%9E%A1%EB%8F%84%EB%93%B1)/)