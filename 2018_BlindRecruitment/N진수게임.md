# N 진수 게임 (2018/+2)

33분 - 1차 디버깅

40분 - 풀이 완료 , 문제점 ~  진법 변환한 숫자가 역순으로 들어가 있었음 

## 문제 분석

>2 ~ 16진법 , 순서가 정해졌을때 제시해야 하는 숫자를 리턴

- 숫자에 대해 진법으로 변환
  - 0 1 10 11 100 ..... 이런식으로 , 무작위 진법에 맞춰서 , 최대갯수 t/n 을 통해서 조정 
  - 10 ~ 16 까지는 문자열변환
  - 숫자도 str 형으로
- 순서에 맞출숴 낼 수 있도록 세팅



## 풀이 과정



- 숫자에 대해 진법으로 변환

  ```
  ex) 100을 2진법으로 변환
  - 100을 넘지 않는 2의 지수를 구함 , 2^6 = 64 , 100 - 2^6 = 36
  - 다시 36을 넘지 않는 2의 지수를 구함 , 2^5 = 32 ,  36 - 32 = 4
  - 다시 4를 넘지 않는 2의 지수를 구함 , 2^2 = 4 , 4 - 4 = 0
  - 0이면 종료  , 최종적으로 1100100
  ```

  2진법은 0 아니면 1이므로  비해 3 ~ 16진법은 1이 아닌 자리수가 존재한다

  자리수는 해당 10진수의 숫자를 넘지않는 진법의 지수를 구한다음에 나눠서 몫을 구하면 됨

  ```
  ex) 51을 16진법으로 변환
  - 16^2 > 51 이므로 51//16 = 3 , 51 - 16*3 = 3 , 즉 2번째자리에 3을 가짐
  - 3 = 3*1 , 3 - 3 = 0 
  - 종료 , 51 = 33(16)
  ```

![Screenshot_178](C:\Users\Ando\Desktop\Capture\Screenshot_178.png)



> 말해야 하는 숫자 리스트로 출력  

![Screenshot_175](C:\Users\Ando\Desktop\Capture\Screenshot_175.png)





## 전체 코드



```python
Alpha = ["A" , "B" , "C" , "D" , "E" , "F"]

def convert_n(num , n):
    
    lst = []
    while(num != 0):
        idx = 0
        while(1):
            if n**(idx + 1) > num: break
            else: idx += 1      
        digit = num // n**idx
        num -= digit*(n**idx)
        lst.append([digit , idx])

    convert_num = ['0' ]* (lst[0][1] + 1)
    for c in lst:
        if c[0] >= 10:
            convert_num[c[1]] = Alpha[c[0] - 10]
        else: convert_num[c[1]] = str(c[0])
    convert_num.reverse()
    return convert_num

def solution(n, t, m, p):
    
    answer = ''
    total_lst = ['0']
    
    # 말해야 하는 숫자 리스트들을 구하자 
    for num in range(1 , t*m):
        total_lst += convert_n(num , n)

    # 말해야하는 숫자를 고르자
    for i in range(t):
        answer += total_lst[m*i + p - 1]
    return answer

```



## 느낀점

```
- 진법 변환만 할 줄 알면 별다른건 없었음
```

