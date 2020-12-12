# CodeSquadMastersCourse_codingtest

## 코드스쿼드 마스터즈 코스 코딩테스트1

word , num, position 안에 단어, 정수, L또는 R을 prompt로 입력받도록 설정했습니다.

split 함수를 통해 문자열 word를 배열에 한글자씩 split 했습니다.

그 후 정수가 양수이면 L,R정방향으로 작동하도록 하였고, 정수가 음수이면 역방향으로 작동하도록 설정했습니다.

shift() 함수를 통해 맨 앞 글자를 담고 push 함수를 통해 담은 그 문자를 뒤에 밀어넣었습니다. 역방향으로 밀때는 맨 뒤 글자를 pop() 해서 a에 담고 맨앞에 unshift를 통해 값을 밀어넣었습니다. 마지막으로 join() 함수를 통해 하나로 합쳐줍니다.
