## sys.stdin

`python`에서 입력을 받을 때 주로 `input()`을 사용한다.
하지만, 많은 수의 입력을 받을 때 `input()`을 사용하면 동작시간이 느려 시간초과로 오답 판정을 받을 수 있다.

이 때는 파이썬 `sys` 라이브러리에 정의되어 있는 `sys.stdin.readline()` 함수를 이용하자.

현재까지 정의되어있는 `입출력` 동작 순서는 다음과 같다.

> `sys.stdin.readline() > raw_input() > input()`

`sys.stdin.readline()`은 한 줄의 문자열을 반환하는데 이것을 `int()`로 묶어서 정수로 변환하는것이 더 빠르다.
`raw_input()`은 문자열을 반환한다.
`input()`은 `raw_input()`을 `evaluate`한 결과를 반환한다.

출처: <a href='https://www.acmicpc.net/board/view/855'>백준</a>

### 📍sys.stdin.readline()
입력한 한 라인을 `interable`에 저장한다.
`띄어쓰기`와 `\n`까지 포함하므로 `split()`을 이용하자.

중간에 `.rstrip()` 붙이는 경우가 많은데 공백을 제거할때 사용하는 함수다. 
보통, 문자열 자체에 변수를 저장하고 싶을 때 많이 사용하지만, `int`, `split()`을 그대로 사용할 수 있다.
즉, `int(sys.stdin.readline())`, `int(sys.stdin.readline().split()` 와 같은 말이다.
쉽게 표현하고 싶으면 input_data = sys.stdin.readline()을 사용하여 코드를 간결하게 하자.