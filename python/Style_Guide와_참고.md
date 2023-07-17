# Style Guide
- Style Guide : 코드의 일관성과 가독성을 향상시키기 위한 규칙과 권장 사항들의 모음
    - 변수명은 무엇을 위한 변수인지 직관적인 이름을 가져야 함
        - 단수/복수도 직관적으로 써주기
        - 상수(변하지않음, 재할당x)는 대문자로!
                
            ex)
                
            ```python
            # 시간 예시
            SECONDS_PER_MINUTE = 60
            MINUTES_PER_HOUR = 60
            HOURS_PER_DAY = 24
            ```
                
    - 공백(spaces) 4칸을 사용하여 코드 블록을 들여쓰기
    - 한 줄의 길이는 79자로 제한하며, 길어질 경우 줄 바꿈을 사용
    - 문자와 밑줄(_)을 사용하여 함수, 변수, 속성의 이름을 작성 (snake case)
    - 함수 정의나 클래스 정의 등의 블록 사이에는 빈 줄을 추가 (붙여쓰지말라는거임)
    - is_(어쩌구) 의 변수는 암묵적으로 true아니면 false임을 판별
    - 등등
        
        [PEP 8 – Style Guide for Python Code | peps.python.org](https://peps.python.org/pep-0008/)
            
- 참고
    - python Tutor : 파이썬 프로그램이 어떻게 실행되는지 도와주는 시각화 도우미
        
        [Python Tutor: Learn Python, JavaScript, C, C++, and Java programming by visualizing code](https://pythontutor.com/)
        
    - 주석 (Comment)
        
        : 프로그램 코드 내에 작성되는 설명이나 메모
        
        인터프리터에 의해 실행되지 않음
        
        ```python
        # 이것은
        age = 10
        
        # 주석입니다
        print(age)
        
        """
        여러 줄 주석
        """
        ```
        
        - 주석의 목적
            - 코드의 특정 부분을 설명하거나 임시로 코드를 비활성화할 때
            - 코드를 이해하거나 문서화하기 위해
            - 다른 개발자나 자신에게 코드의 의도나 동작을 설명하는 데 도움