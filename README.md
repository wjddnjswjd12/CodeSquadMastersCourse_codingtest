# CodeSquadMastersCourse_codingtest

## 코드스쿼드 마스터즈 코스 코딩테스트3

---

STEP-3 코드 입니다. 문제가 너무 어려워서 구현하는 데에 급급하여 코드가 매우 깁니다...모르겠어서 하나 하나 다 무식하게 돌려보는 식으로 구현을 해서요.

아직 제 실력으론 짧고 코드를 간결하게 요약하기가 어려웠습니다... 읽기 어려운 점 너그럽게 이해해주시면 감사하겠습니다. 그대신 README.md를 읽고 이해하실 수 있도록 자세하게 설명해두겠습니다.

---

rubiks 라는 객체를 생성하여 그 안에 B,W,O,G,Y,R 배열을 각각 생성했습니다.
그리고 rubiks.main 메소드를 큰 틀로 사용하여 전반적인 코드 작동을 제어했습니다.

```Javascript
  rubiks = {
        B: [
          ["B", "B", "B"],
          ["B", "B", "B"],
          ["B", "B", "B"],
        ],
        W: [
          ["W", "W", "W"],
          ["W", "W", "W"],
          ["W", "W", "W"],
        ],
        O: [
          ["O", "O", "O"],
          ["O", "O", "O"],
          ["O", "O", "O"],
        ],
        G: [
          ["G", "G", "G"],
          ["G", "G", "G"],
          ["G", "G", "G"],
        ],
        Y: [
          ["Y", "Y", "Y"],
          ["Y", "Y", "Y"],
          ["Y", "Y", "Y"],
        ],
        R: [
          ["R", "R", "R"],
          ["R", "R", "R"],
          ["R", "R", "R"],
        ],
```

```Javascript

      rubiks.main = function () {
        var start = new Date().getTime();
        this.showCube(this.B, this.W, this.O, this.G, this.Y, this.R);
        var vocabs = this.wordsplit(this.word);
        if (this.word === "Q") {
          document.write("CUBE> " + this.word);
          document.write("이용해 주셔서 감사합니다. 뚜뚜뚜.");
        } else {
          document.write("CUBE> " + this.word);
          this.moveCube(vocabs);
          elapsed = new Date().getTime() - start;
          document.write("소요된 시간: " + elapsed + "초<br>");
          document.write("조작갯수: " + vocabs.length + "<br>");
          document.write("이용해 주셔서 감사합니다. 뚜뚜뚜.");
        }
      };

      rubiks.main();
```

var start 에 시작시간을 담았습니다. 나중에 끝난 시간은 elapsed 변수에 담았습니다.

```Javascript
this.showCube(this.B, this.W, this.O, this.G, this.Y, this.R);
```

화면의 맨 윗부분에 보일 큐브 6면을 먼저 출력했습니다.

rubiks.showCube() 함수를 보면,

```Javascript
showCube: function (B, W, O, G, Y, R) {
          B.forEach((value) =>
            document.write(
              "&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;" +
                value.join(" ") +
                "<br>"
            )
          );
          document.write("<br>");
          for (var i = 0; i < W.length; i++) {
            document.write(
              W[i].join(" ") +
                "&emsp;&emsp;" +
                O[i].join(" ") +
                "&emsp;&emsp;" +
                G[i].join(" ") +
                "&emsp;&emsp;" +
                Y[i].join(" ") +
                "<br>"
            );
          }
          document.write("<br>");
          R.forEach((value) =>
            document.write(
              "&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;" +
                value.join(" ") +
                "<br>"
            )
          );
          document.write("<br>" + "<br>");
        }
```

출력할 배열 6개를 불러와서 각각 출력을 해줍니다. 좀 더 깔끔하게 출력하기 위해서 join("공백") 메소드를 사용하여 배열을 공백을 사이로 둔 문자열로 합쳐서 출력하였습니다.

```Javascript
 var vocabs = this.wordsplit(this.word);
```

vocabs 라는 변수안에 this.wordsplit(this.word) 반환값을 넣어줬습니다.
이때 this.word 는 rubiks.word로 prompt로 문자열을 입력받았습니다.

```Javascript
word: prompt("CUBE>"),
```

입력받은 rubiks.word 값을 wordsplit 메소드에 넘깁니다.

```Javascript
wordsplit: function (strings) {
          var temp = strings.split("");
          var isNum = /[0-9]/;
          var isEng = /[a-zA-Z]/; //regex test()메소드
          var array = [];
          while (temp.length > 0) {
            for (var i = 0; i < temp.length; i++) {
              if (isEng.test(temp[i]) && temp[i + 1] == "'") {
                if (isNum.test(temp[i + 2])) {
                  var temp2 = temp.splice(i, 3).join("");
                  array.push(temp2);
                } else {
                  var temp2 = temp.splice(i, 2).join("");
                  array.push(temp2);
                }
                break;
              } else if (isEng.test(temp[i]) && temp[i + 1] !== "'") {
                if (isNum.test(temp[i + 1])) {
                  var temp2 = temp.splice(i, 2).join("");
                  array.push(temp2);
                } else {
                  var temp2 = temp.splice(i, 1).join("");
                  array.push(temp2);
                }
                break;
              }
            }
          }
          return array;
        },
```

---

어떻게하면 R, R', R2, R2' 를 각각 분리해서 배열에 넣을 수 있을까 고민하다가, regexp의 test()메소드가 있다는 것을 알게되어 그 방법을 사용했습니다.

```Javascript
          var temp = strings.split("");
          var isNum = /[0-9]/;
          var isEng = /[a-zA-Z]/; //regex test()메소드
          var array = [];
          .
          .
          .
           if (isEng.test(temp[i]) && temp[i + 1] == "'") {
                if (isNum.test(temp[i + 2])) {
                  var temp2 = temp.splice(i, 3).join("");
                  array.push(temp2);
                } else {
                  var temp2 = temp.splice(i, 2).join("");
                  array.push(temp2);
                }
                break;

```

일단 temp안에 문자열을 split("") 메소드로 하나씩 분리했습니다.
그리고 isNum은 숫자, isEng은 알파벳을 test하도록 설정했습니다.

if(temp[i]가 알파벳이면서 && temp[i]의 다음 값에 '가 있을때) 즉, U' 같은 경우.

그리고 그런 조건에 또 다른 조건으로 if(temp[i]의 다음다음 값에 숫자가 있다면) 즉 U'3 같은 경우,

splice 함수를 통해 빈 배열 temp2에 temp[i]부터 3개를 빼내와서 담습니다.
그리고 미리 선언해둔 빈 array배열에 그 값을 push 합니다.

else 부분은 U'처럼 (알파벳+ ')인데 뒤에 숫자가 없을 경우를 뜻합니다. 저 경우에도 temp2에 splice 함수로 temp[i]위치에서부터 2개를 빼내온다음에 그것을 array에 push합니다.

그리고 break함수를 써서 for문만 빠져나옵니다.

```Javascript
else if (isEng.test(temp[i]) && temp[i + 1] !== "'") {
                if (isNum.test(temp[i + 1])) {
                  var temp2 = temp.splice(i, 2).join("");
                  array.push(temp2);
                } else {
                  var temp2 = temp.splice(i, 1).join("");
                  array.push(temp2);
                }
                break;
```

이부분은 else if (temp[i]가 알파벳이면서 바로 뒤의 값에 '가 없을경우, 즉 U 일경우)

이면서 2중조건으로 if(temp[i]의 다음값이 숫자일 경우, U2 같은 경우)
비슷한 맥락으로 temp2에 splice함수로 값을 담은후 array에 push 합니다.

만약 조건이 충족되어 함수들이 다실행 되면 break 문을 통해 for문만 빠져나옵니다.
그리고 이 과정을 while문으로 감싸서 temp.length가 0이 아닐때까지 반복합니다. splice함수 때문에 temp에는 언젠가 값이 모두 사라집니다.

while문이 끝나면 return array를 통해 잘 분리된 배열을 반환합니다.

example) UU'LB2B' => [" U " , " U' " , " L " , " B2 " , " b' "]

---
