# CodeSquadMastersCourse_codingtest

#코드스쿼드 마스터즈 코스 코딩테스트2

cube 라는 객체 생성 후
initialCube에 맨 위에 미리보기로 띄울 값을 넣었습니다.

그 후 직접적으로 변화를 줄 arr2라는 객체에 initialCube와 같은 값들을 넣었습니다.

cube.word 에 prompt 로 입력을 받고, wordSplit 이라는 함수로 하나씩 분리했습니다.
예를들면 ("U'BL'"=>["U'","B","L"]) 이런식으로 했습니다.

```Javascript
wordSplit: function (strings) {
          var temp = strings.split("");
          var array = [];
          while (temp.length > 0) {
            for (var i = 0; i < temp.length; i++) {
              if (temp[i] !== "'" && temp[i + 1] == "'") {
                var temp2 = temp.splice(i, 2).join("");
                array.push(temp2);
                break;
              } else if (temp[i] !== "'" && temp[i + 1] !== "'") {
                var temp2 = temp.splice(i, 1).join("");
                array.push(temp2);
                break;
              }
            }
          }
          return array;
        }
```

word.Split함수의 매개변수로 문자열을 받아와서 var temp에 split("")함수를 통해 하나씩 쪼개고, ' 가 아닌 값이면서(즉 알파벳) 뒤에 '를 가진 (U') 값이면 splice함수로 그 둘을 빼내와서 temp2에 담았습니다. 그 후 미리 만들어둔 array배열에 하나씩 push 했습니다.
