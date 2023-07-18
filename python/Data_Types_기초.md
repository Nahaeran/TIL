# Data Types

Data Types : 값의 종류와 그 값에 적용 가능한 연산과 동작을 결정하는 속성

> 데이터 타입이 필요한 이유
>
> - 값들을 구분하고, 어떻게 다뤄야 하는지를 알 수 있음
> - 요리 재료마다 특정한 도구가 필요하듯이 각 데이터 타입 값들도 각자에게 적합한 도구를 가짐
> - 타입을 명시적으로 지정하면 코드를 읽는 사람이 변수의 의도를 더 쉽게 이해할 수 있고, 잘못된 데이터 타입으로 인한 오류를 미리 예방

# Numeric Types

1. int (정수 자료형) : 정수를 표현하는 자료형

   - 2진수(binary) : 0b
   - 8진수(octal) : 0o
   - 16진수(hexadecimal) : 0x

     ```python
     # n진수에서 10진수로
     print(0b10) # 2
     print(0o30) # 24
     print(0x10) # 16

     # 10진수에서 n진수로
     print(bin(12)) # 0b110
     print(oct(12)) # 0o14
     print(hex(12)) # 0xc
     ```

2. float (실수 자료형) : 실수를 표현하는 자료형 프로그래밍 언어에서 float는 실수에 대한 근삿값임

   - 유한 정밀도
     - 컴퓨터 메모리 용량이 한정돼 있고 한 숫자에 대해 저장하는 용량이 제한 됨
     - 0.6666666666666666과 1.6666666666666667은 제한된 양의 메모리에 저장할 수 있는 2/3과 5/3에 가장 가까운 값
   - 실수 연산 시 주의사항
     - 컴퓨터는 2진법를 사용, 사람은 10진법을 사용
     - 이때 10진수 0.1은 2진수로 표현하면 0.00011001100110011001100..같이 무한대로 반복
     - 무한대 숫자를 그대로 저장할 수 없어서 사람이 사용하는 10진법의 근사값만 표시
     - 0.1의 경우 3602879701896397 / 2 \*\* 55 이며 0.1에 가깝지만 정확히 동일하지는 않음
     - 이런 과정에서 예상치 못한 결과가 나타남
     - 이런 증상을 Floating point rounding error라고 함
   - 실수 연산 시 해결책
     - 두 수의 차이가 매우 작은 수보다 작은지를 확인하거나 math모듈 활용
       ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/87462b3b-15bf-44d8-8ad3-2ebfdc1c5dfd/Untitled.png)
   - 지수 표현 방식 (10^)

     - e 또는 E를 사용한 지수 표현

       ```python
       # 314 * 0.01
       number = 314e-2
       number2 = 314e2

       # float
       print(type(number))
       print(type(number2))

       print(number) # 3.14
       print(number2) # 31400.0
       ```

# Sequence Type

Sequence Type : 여러 개의 값들을 순서대로 나열하여 저장하는 자료형 (str, list, tuple, range)

> **_Sequence Type의 특징_**
>
> 1. 순서(Sequence) : 값들이 순서대로 저장 (정렬X)
> 2. 인덱싱(Indexing) : 각 값에 고유한 인덱스(번호)를 가지고 있으며, 인덱스를 사용하여 특정 위치의 값을 선택하거나 수정할 수 있음
> 3. 슬라이싱(Slicing) : 인덱스 범위를 조절해 부분적인 값을 추출할 수 있음
> 4. 길이(Length) : len() 함수를 사용하여 저장된 값의 개수(길이)를 구할 수 있음
> 5. 반복(Iteration) : 반복문을 사용하여 저장된 값들을 반복적으로 처리할 수 있음

1.  str (문자열) : 문자들의 순서가 있는 변경 불가능한 시퀀스 자료형

    - 문자열 표현
      - 문자열은 단일 문자나 여러 문자의 조합으로 이루어짐
      - 작은따옴표 (’) 또는 큰따옴표 (”)로 감싸서 표현
    - 중첩 따옴표
      - 따옴표 안에 따옴표를 표현할 경우
        - 작은따옴표가 들어 있는 경우는 큰따옴표로 문자열 생성
        - 큰따옴표가 들어 있는 경우는 작은따옴표로 문자열 생성
    - Escape sequence

      - 역슬래시 (backslash) 뒤에 특정 문자가 와서 특수한 기능을 하는 문자 조합
      - 파이썬의 일반적인 문법 규칙을 잠시 탈출한다는 의미
        | 예약문자 | 내용(의미) |
        | -------- | ----------- |
        | \n | 줄 바꿈 |
        | \t | 탭 |
        | \\ | 백슬래시 |
        | \’ | 작은 따옴표 |
        | \” | 큰 따옴표 |
      - 예시

        ```python
        # 철수야 '안녕'
        print('철수야 \'안녕\'')

        '''
        이 다음은 엔터
        입니다.
        '''
        print('이 다음은 엔터\n입니다.'
        ```

    - String Interpolation : 문자열 내에 변수나 표현식을 삽입하는 방법

      - f-string

        - 문자열에 f 또는 F 접두어를 붙이고 표현식을 {expression}로 작성하여 문자열에 파이썬 표현식의 값을 삽입할 수 있음

          ```python
          bugs = 'roaches'
          counts = 13
          area = 'living room'

          # Debugging roaches 13 living room
          print(f'Debugging {bugs} {counts} {area}')
          ```

        - f-string 응용 (f-string advanced 라고 검색하기)

          ```python
          # 10칸 중에 가운데 두칸을 hi가 차지하도록
          greeting = 'hi'
          print(f'{greeting:^10}')

          # 10칸 중에 오른쪽 두칸을 hi가 차지하도록
          print(f'{greeting:>10}')

          # 소숫점 다섯번째에서 반올림하여 네번째까지 출력
          print(f'{3.141592:.4f}')
          ```

    - 문자열 시퀀스 특징

      ```python
      my_str = 'hello'

      # 인덱싱
      print(my_str[1]) # e

      # 슬라이싱
      print(my_str[2:4] # ll

      # 길이
      print(len(my_str)) # 5
      ```

    - 문자열은 불변 (변경 불가)

      ````python
      my_str = 'hello'

           # TypeError : 'str' object does not support item assignment
           my_str[1] = 'z'
           ```
           → 필요시, 새로운 문자열을 만들어낼 생각으로 문제에 접근

      > 인덱스(Index) : 시퀀스 내의 값들에 대한 고유한 번호로, 각 값의 위치를 식별하는 데 사용되는 숫자
      >
      > |       | h   | e   | l   | l   | o   |
      > | ----- | --- | --- | --- | --- | --- |
      > | index | 0   | 1   | 2   | 3   | 4   |
      > | index | -5  | -4  | -3  | -2  | -1  |
      ````

> 슬라이싱(slicing) : 시퀀스의 일부분을 선택하여 추출하는 작업
>
> → 시작 인덱스와 끝 인덱스를 지정하여 해당 범위의 값을 포함하는 새로운 시퀀스를 생성
>
> - slicing 예시 `my_str[2:4]` > ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/49902072-b9c3-46ba-9a8e-91eeeaa33fa2/Untitled.png)
> - slicing 예시 `my_str[:3]` > ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/11fcabd8-24fa-4e5b-b96d-eaa32ce52ea0/Untitled.png)
> - slicing 예시 `my_str[3:]` > ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/d6b1ed3e-fe54-47dd-93ff-01e25d4a0327/Untitled.png)
> - slicing 예시 `my_str[0:5:2]` step을 지정하여 추출
>   ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/4e0a8e04-bc44-4d17-a676-75820ded8fd0/Untitled.png)
> - slicing 예시 `my_str[::-1]` step이 음수일 경우? 문자열 뒤집기!
>   ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/f61f713f-3b68-4da0-b416-829b66dc4a63/Untitled.png)

2. list (리스트) : 여러 개의 값을 순서대로 저장하는 변경 가능한 시퀀스 자료형

   - 리스트 표현
     - 0개 이상의 객체를 포함하며 데이터 목록을 저장
     - 대괄호([])로 표기
     - 데이터는 어떤 자료형도 저장할 수 있음
       ```python
       my_list1 = []
       my_list_2 = [1, 'a', 3, 'b', 5]
       my_list_3 = [1, 2, 3, 'Python', ['hello', 'world', '!!!']]
       ```
   - 리스트의 시퀀스 특징

     ```python
     my_list = [1, 'a', 3, 'b', 5]

     # 인덱싱
     print(my_list[1]) # a

     # 슬라이싱
     print(my_list[2:4]) # [3, 'b']
     print(my_list[:3]) # [1, 'a', 3]
     print(my_list[3:]) # ['b', 5]
     print(my_list[0:5:2]) # [1, 3, 5]
     print(my_list[::-1]) # [5, 'b', 3, 'a', 1]

     #길이
     print(len(my_list)) # 5
     ```

   - 중첩된 리스트 접근

     ```python
     my_list = [1, 2, 3, 'Python', ['hello', 'world', '!!!']]

     print(len(my_list)) # 5
     print(my_list[4][-1]) # !!!
     print(my_list[-1][1][0]) # w
     ```

   - 리스트는 가변 (변경 가능)

     ```python
     my_list = [1, 2, 3]
     my_list[0] = 100

     print(my_list) # [100, 2, 3]
     ```

3. tuple (튜플) : 여러 개의 값을 순서대로 저장하는 변경 불가능한 시퀀스 자료형

   → list랑 똑같은데 변경 불가능함!

   - 튜플 표현
     - 0개 이상의 객체를 포함하며 데이터 목록을 저장
     - 소괄호 (())로 표기
     - 데이터는 어떤 자료형도 저장할 수 있음
       ```python
       my_tuple_1 = ()
       my_tuple_2 = (1, )
       my_tuple_3 = (1, 'a', 3, 'b', 5)
       ```
   - 튜플의 시퀀스 특징

     ```python
     my_tuple_3 = (1, 'a', 3, 'b', 5)

     # 인덱싱
     print(my_tuple[1]) # a

     #슬라이싱
     print(my_tuple[2:4]) # (3, 'b')

     #길이
     print(len(my_tuple)) # 5
     ```

   - 튜플은 불변 (변경 불가)

     ```python
     my_tuple = (1, 'a', 3, 'b', 5)

     # TypeError : 'tuple' object does not support item assignment
     my_tuple[1] = 'z'
     ```

   - 튜플은 어디에 쓰일까?

     - 튜플의 불변 특성을 사용한 안전하게 여러 개의 값을 전달, 그룹화, 다중 할당 등 개발자가 직접 사용하기 보다 ‘파이썬 내부 동작’에서 주로 사용됨

       ```python
       x, y = (10, 20)

       print(x) # 10
       print(y) # 20

       # 파이썬은 쉼표를 튜플 생성자로 사용하니 괄호는 생략 가능
       x, y = 10, 20
       ```

4. range : 연속된 정수 시퀀스를 생성하는 변경 불가능한 자료형

   range는 함수이기도 하지만 자료형이기도 함

   - range 표현

     - `range(n)`
       - 0부터 n-1까지의 숫자 시퀀스
     - `range(n, m)`
       - n부터 m-1까지의 숫자 시퀀스

     ```python
     my_range_1 = range(5)
     my_range_2 = range(1, 10)

     print(my_range_1) # range(0, 5)
     print(my_range_2) # range(1, 10)
     ```

     - 주로 반복문과 함께 사용 예정

       ```python
       my_range_1 = range(5)
       my_range_2 = range(1, 10)

       print(my_range_1) # range(0, 5)
       print(my_range_2) # range(1, 10)

       print(list(my_range_1)) # [0, 1, 2, 3, 4]
       print(list(my_range_2)) # [1, 2, 3, 4, 5, 6, 7, 8, 9]
       ```

# Non-sequence Types

1. dict (딕셔너리) : key-value 쌍으로 이루어진 순서와 중복이 없는 변경 가능한 자료형

   - 딕셔너리 표현

     - key는 변경 불가능한 자료형만 사용 가능 (str, int, float, tuple, range …)
     - value는 모든 자료형 사용 가능
     - 중괄호 ({})로 표기

       ```python
       my_dict_1 = {}
       my_dict_2 = {'key' : 'value'}
       my_dict_3 = {'apple' : 12, 'list' : [1, 2, 3]}

       print(my_dict_1) # {}
       print(my_dict_2) # {'key' : 'value'}
       print(my_dict_3) # {'apple' : 12, 'list' : [1, 2, 3]}
       ```

   - 딕셔너리 사용

     - key를 통해 value에 접근

       ```python
       my_dict_3 = {'apple' : 12, 'list' : [1, 2, 3]}

       print(my_dict['apple']) # 12
       print(my_dict['list']) # [1, 2, 3]

       # 값 변경
       my_dict['apple'] = 100
       print(my_dict) # {'apple' : 12, 'list' : [1, 2, 3]}
       ```

2. set (세트) : 순서와 중복이 없는 변경 가능한 자료형

   - 세트 표현

     - 수학에서의 집합과 동일한 연산 처리 가능
     - 중괄호 ({})로 표기

       ```python
       my_set_1 = set() # 딕셔너리와 표현법 중복을 막기위해
       my_set_2 = {1, 2, 3}
       my_set_3 = {1, 1, 1}

       print(my_set_1) # set()
       print(my_set_1) # {1, 2, 3}
       print(my_set_1) # {1}
       ```

   - 세트의 집합 연산

     ```python
     my_set_1 = {1, 2, 3}
     my_set_2 = {3, 6, 9}

     # 합집합
     print(my_set_1 | my_set_2) # {1, 2, 3, 6, 9}

     # 차집합
     print(my_set_1 - my_set_2) # {1, 2}

     # 교집합
     print(my_set_1 & my_set_2) # {3}
     ```

# Other Types

1. None : 파이썬에서 ‘값이 없음’을 표현하는 자료형
   - None 표현
     ```python
     variable = None
     print(variable) # None
     ```
2. Boolean : 참(True)과 거짓(False)을 표현하는 자료형

   - 불리언 표현

     - 비교 / 논리 연산의 평가 결과로 사용됨
     - 주로 조건 / 반복문과 함께 사용

       ```python
       bool_1 = True
       bool_2 = False

       print(bool_1) # True
       print(bool_2) # False
       print(3 > 1) # True
       print('3' != 3) # True
       ```

# Collection

Collection : 여러 개의 항목 또는 요소를 담는 자료 구조 (str, list, tuple, set, dict)

- 컬렉션 정리
  | 컬렉션 | 변경 가능 여부 | 순서 여부 |
  | ------ | -------------- | --------- |
  | str | X | O |
  | list | O | O |
  | tuple | X | O |
  | set | O | X |
  | dict | O (key는 안됨) | X |
- 불변과 가변의 차이

  ```python
  my_str = 'hello'
  # TypeError : 'str' object does not support item assignment
  my_str[0] = 'z'

  my_list = [1, 2, 3]
  my_list[0] = 100
  # [100, 2, 3]
  print(my_list)
  ```

  가변이라는 것은? 안에 있는 것의 참조의 방향을 바꾸면 됨. (리스트는 객체들의 참조를 모아놓은 컬렉션이라고 부르기도 함)
  하지만 문자열은 문자열이 통째로 메모리 주소 하나에 저장되기 때문에 불변이다.
  ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/ccedeb54-f170-4ed5-a557-8ef24fe51e7f/Untitled.png)

# Type Conversion

- 암시적 형변환 (Implicit Type conversion) : (필요할때 or 참과 거짓을 판단할때) 파이썬이 자동으로 형변환(값 자체를 바꾸는 것이 아님)을 하는 것
  값이 있으면 → True 예시) 1, 3, ‘ ‘, “hi”
  값이 없는 경우 → False 예시) 0, ‘’, [], {}, ()
  - 암시적 형변환 예시
    - Boolean과 Numeric Type에서만 가능
    ```python
    print(3 + 5.0) # 8.0
    print(True + 3) # 4
    print(True + False) # 1
    ```
- 명시적 형변환 (Explicit Type conversion) : 개발자가 직접 형변환을 하는 것, 암시적 형변환이 아닌 경우를 모두 포함

  - 명시적 형변환 예시

    - str → integer : 형식에 맞는 숫자만 가능
    - integer → str : 모두 가능

    ```python
    print(int('1')) # 1
    print(str(1) + '등') # 1등
    print(float('3.5')) # 3.5
    print(int(3.5)) # 3

    # ValueError : invalid literal for int() with base 10: '3.5'
    print(int('3.5'))
    ```

- 컬렉션 간 형변환 정리
  str→list 가능 str→range 불가능
  | | str | list | tuple | range | set | dict |
  | ----- | --- | --------- | --------- | ----- | --------- | ---- |
  | str | | O | O | X | O | X |
  | list | O | | O | X | O | X |
  | tuple | O | O | | X | O | X |
  | range | O | O | O | | O | X |
  | set | O | O | O | X | | X |
  | dict | O | O (key만) | O (key만) | X | O (key만) | |
