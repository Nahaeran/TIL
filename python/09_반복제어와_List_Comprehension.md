# 반복 제어
    
반복 제어 : for문과 while은 매 반복마다 본문 내 모든 코드를 실행하지만 때때로 일부만 실행하는 것이 필요할 때가 있음
    
- `break` : 반복을 즉시 중지
    - `break` 예시
        - 프로그램 종료 조건 만들기
                
            ```python
            number = int(input('양의 정수를 입력해주세요. : '))
                
            while number <= 0:
                if number == -9999:
                	print('프로그램을 종료합니다.')
                	break
                	
                if number < 0:
                	print('음수를 입력했습니다.')
                else:
                	print('0은 양의 정수가 아닙니다.')
                	
                number = int(input('양의 정수를 입력해주세요. : '))
                
            print('잘했습니다!')
                
            """
            양의 정수를 입력해주세요. : -9999
            프로그램을 종료합니다.
            잘했습니다!
            """
            ```
                
        - 리스트에서 짝수 찾아서 출력하기
                
            ```python
            numbers = [1, 3, 5, 6, 7, 9, 10, 11]
            found_even = False
                
            for num in numbers:
                if num % 2 == 0:
                	print('첫 번째 짝수를 찾았습니다 : ', num)
                	found_even = True
                	break
                
            if not found_even:
                print('짝수를 찾지 못했습니다.')
                
            """
            첫 번째 짝수를 찾았습니다 : 6
            """
            ```
                
- `continue` : 다음 반복으로 건너뜀
    - `continue` 예시
    - 현재 반복문의 남은 코드를 건너뛰고 다음 반복으로 넘어감
            
        ```python
        numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
            
        for num in numbers:
            if num % 2 == 0:
            	continue
            print(num)
            
        """
        1
        3
        5
        7
        9
        """
        ```
            
        
- `break`와 `continue` 주의사항
    - break와 continue를 남용하는 것은 코드의 가독성을 저하시킬 수 있음
    - **특정한 종료 조건**을 만들어 break를 대신하거나, ***if문을 사용***해 continue처럼 코드를 건너뛸 수도 있음
    - 약간의 시간이 들더라도 가능한 코드의 가독성을 유지하고 코드의 의도를 명확하게 작성하도록 노력하는 것이 중요
        
    ```python
    for number in range(1, 5):
        if number == 3:
        	continue
        print(number)
    """
    1
    2
    4
    """
        
    for number in range(1, 5):
        if number != 3:
        	print(number)
    """
    1
    2
    4
    """
    ```
        
# List Comprehension
    
List Comprehension  : 간결하고 효율적인 리스트 생성 방법
    
- List Comprehension 구조
        
    ```python
    [expression for 변수 in iterable]
    list(expression for 변수 in iterable)
    ```
        
- List Comprehension 활용
        
    ```python
    # 사용 전
    numbers = [1, 2, 3, 4, 5]
    squared_numbers = []
        
    for num in numbers:
        squared_numbers.append(num ** 2)
        
    print(squared_numbers) # [1, 4, 9, 16, 25]
        
    # 사용 후
    numbers = [1, 2, 3, 4, 5]
    squared_numbers = [num ** 2 for num in numbers]
        
    print(squared_numbers) # [1, 4, 9, 16, 25]
    ```
        
- [참고] List Comprehension과 if 조건문
        
    ```python
    [expression for 변수 in iterable if 조건식]
    list(expression for 변수 in iterable if 조건식)
    ```
        
- 하지만! List Comprehension도 남용하지말자…
        
    “Simple is better than complex”, “Keep it simple, stupid”
        
- 리스트를 생성하는 3가지 방법 비교
    - 어떤게 제일 빨라요?? → 외부요인이 너무 많아서 일반화가 불가능함
            
        하지만 여러 사람들이 분석한 결과
            
        대부분의 상황에서는 comprehension이 빠르다
            
        하지만 다른 함수, 내장 함수에 따라 map이 더 빠른 경우도 많았다.
        
        파이썬이 3점대 후반ver에서 for loop 성능에 비약적인 향상이 있었음
            
        ⇒ 그래서 극단적인 차이는 존재하지 않는다..
            
        프로그래밍은 우리 프로그램이 어떻게 그 목적을 명확하게 전달하는지에 대한 것, 코드의 가독성이 제일 중요하다.
            
        > 작은 효율성에 대해서는, 말하자면 97% 정도에 대해서는, 잊어버려라. 섣부른 최적화는 모든 악의 근원이다. - Donald E. Knuth
        > 
        1. for loop
                
            ```python
            numbers = ['1', '2', '3']
            new_numbers = []
                
            for number in numbers:
                new_numbers.append(int(number))
            print(new_numbers) # [1, 2, 3]
            ```
                
        2. map
                
            ```python
            numbers = ['1', '2', '3']
            new_numbers_2 = list(map(int, numbers))
            print(new_numbers_2) # [1, 2, 3]
            ```
                
        3. List comprehension
                
            ```python
            numbers = ['1', '2', '3']
            new_numbers_3 = [int(number) for number in numbers]
            print(new_numbers_3) # [1, 2, 3]
            ```
                
# 참고
- `pass`
    - 아무런 동작도 수행하지 않고 넘어가는 역할 (자리 차지하는 역할)
    - 문법적으로 문장이 필요하지만 프로그램 실행에는 영향을 주지 않아야 할 때 사용
    - `pass` 예시
        1. 코드 작성 중 미완성 부분
            - 구현해야 할 부분이 나중에 추가될 수 있고, 코드를 컴파일하는 동안 오류가 발생하지 않음
                    
                ```python
                def my_function():
                    pass
                ```
                    
        2. 조건문에서 아무런 동작을 수행하지 않아야 할 때
                
            ```python
            if condition:
                pass # 아무런 동작도 수행하지 않음
            else:
                # 다른 동작 수행
            ```
                
        3. 무한 루프에서 조건이 충족되지 않을 때 pass를 사용하여 루프를 계속 진행하는 방법
                
            ```python
            while True:
                if condition:
                	break
                elif condition:
                	pass # 루프 계속 진행
                else:
                	print('..')
            ```
                
    - `pass` vs `continue`
        - pass는 그저 자리차지
        - continue는 반복을 넘어가주는 역할
                
            ⇒ 하는일이 전혀 다름!
                
- `enumerate`
    - `enumerate(iterable, start=0)`
            
        ```python
        fruits = ['apple', 'banana', 'cherry']
            
        for index, fruit in enumerate(fruits):
            print(f'인덱스 {index}: {fruit}')
            
        """
        인덱스 0: apple
        인덱스 1: banana
        인덱스 2: cherry
        """
            
        print(enumerate(fruits)) # <enumerate object at 0x0000026995480FC0>
        print(list(enumerate(fruits))) # [(0, 'apple'), (1, 'banana'), (2, 'cherry')]
        ```