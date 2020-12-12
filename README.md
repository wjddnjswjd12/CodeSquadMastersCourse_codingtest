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

다시 메인 함수로 돌아와서,

```Javascript
 rubiks.main = function () {
                              .
                              .
                              .
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

```

wordsplit 메소드의 반환값으로 받아온 배열 vocabs를 moveCube 에 넘기기 전에, 입력한 값이 Q인지 아닌지 판별하여 각 다른 결과를 출력하도록 설정했습니다.

else 이후에 this.moveCube(vocabs); 메소드를 실행시킵니다. 본격적으로 큐브를 이동시키는 부분이 시작됩니다. moveCube 메소드를 보기전에 봐야 할 메소드 2개가 있습니다.

```Javascript
        cubeSplitMoveUL: function (a1, a2, a3, a4) {
          var temp = [];
          temp.push(a1, a2, a3, a4);
          var temp2 = [];
          temp2 = temp.shift();
          temp.push(temp2);
          return temp;
        }, //큐브면 움직이기 방향: 위,왼쪽

        cubeSplitMoveDR: function (a1, a2, a3, a4) {
          var temp = [];
          temp.push(a1, a2, a3, a4);
          var temp2 = [];
          temp2 = temp.pop();
          temp.unshift(temp2);
          return temp;
        }, //큐브면 움직이기 방향: 아래,오른쪽
```

rubiks.cubeSplitMoveUL 메소드는 큐브 면의 이동 방향이 윗방향, 왼쪽방향 일 때 불러와 작동합니다. 예를들면 **(F',R,U,B,L',D')** 회전들은 면이 윗방향으로 회전하거나 왼쪽으로 회전합니다

일단 값이 바뀌는 4개의 면을 배열로 받아옵니다.

이때 면이란 ▣▣▣▣ 한 줄들을 의미합니다. 예를들면 U 회전의 경우 맨윗면의 4개의 큐브들만 서로 회전이동합니다.

받아온 배열들을 빈 배열 temp에 하나씩 push 합니다. 그리고 다른 빈 배열 temp2 에 temp의 맨 앞 값을 shift으로 빼내오고, 빼내온 값을 push()메소드로 맨 뒤에 집어넣습니다.

비슷한 방식으로 rubiks.cubeSplitMoveDR 은 메소드는 큐브 면의 이동 방향이 아랫방향, 오른쪽방향 일 때 불러와 작동합니다. 예를들면 **(F,R',U',B',L,D)** 회전들은 면이 아랫방향으로 회전하거나 오른쪽으로 회전합니다

이 때 불러온 배열을 temp에 하나씩 push 하고, 다른 빈 배열 temp2에 temp의 맨 마지막 값을 pop()으로 빼내옵니다. 그리고 빼내온 값을 unshift()메소드를 통해 맨 앞에 집어넣었습니다.

---

---

---

이제 moveCube메소드를 설명하겠습니다.

```Javascript
 rubiks.moveCube: function (alpha) {
          for (var x = 0; x < alpha.length; x++) {
            if (alpha[x].includes("F") && !alpha[x].includes("'")) {
                    .
                    .
                    .

     },
      };

```

일단 큰 틀로 전체 함수가 어떻게 작동하는지 설명하겠습니다. alpha에는 아까 main함수에서 입력한 UU'R'2L 같은 문자열을 배열로 쪼갠 값을 불러옵니다.

만약 alpha가 ["U","U',"R'2","L] 일때, alpha의 각 값들(예를들면 alpha[0]="U")을 for문을 통해 순서대로 이동시킵니다.

그 후 어떤 문자를 입력했는지에 따라 if문으로 나눴습니다.

```Javascript
 if (alpha[x].includes("F") && !alpha[x].includes("'")) {
              //F F2 F3...
              var num;
              alpha[x][1] ? (num = alpha[x][1]) : (num = 1); //횟수를 가리키는 숫자가 있다면 num=숫자 아니면 num=1
              for (var i = 0; i < num; i++) {
                var arr2 = [];
                arr2 = this.cubeSplitMoveDR(
                  this.B[2],
                  [this.G[0][0], this.G[1][0], this.G[2][0]],
                  this.R[0],
                  [this.W[0][2], this.W[1][2], this.W[2][2]]
                );

                this.B[2] = arr2[0];
                this.G[0][0] = arr2[1][0];
                this.G[1][0] = arr2[1][1];
                this.G[2][0] = arr2[1][2];
                this.R[0] = arr2[2];
                this.W[0][2] = arr2[3][0];
                this.W[1][2] = arr2[3][1];
                this.W[2][2] = arr2[3][2];
              }
            } else if (alpha[x].includes("F'")) {
              //F' F'2 F'3...
              var num;
              alpha[x][2] ? (num = alpha[x][2]) : (num = 1);
              for (var i = 0; i < num; i++) {
                var arr2 = [];
                arr2 = this.cubeSplitMoveUL(
                  this.B[2],
                  [this.G[0][0], this.G[1][0], this.G[2][0]],
                  this.R[0],
                  [this.W[0][2], this.W[1][2], this.W[2][2]]
                );

                this.B[2] = arr2[0];
                this.G[0][0] = arr2[1][0];
                this.G[1][0] = arr2[1][1];
                this.G[2][0] = arr2[1][2];
                this.R[0] = arr2[2];
                this.W[0][2] = arr2[3][0];
                this.W[1][2] = arr2[3][1];
                this.W[2][2] = arr2[3][2];
              }
            }
```

F와 F'회전 코드입니다.

---

if (alpha[x].includes("F") && !alpha[x].includes("'"))이부분의 뜻은 if(alpha[x] 안에 F를 포함하고 있으면서, '가 없을 때, 즉 F일때 를 뜻합니다.)

alpha[x][1] ? (num = alpha[x][1]) : (num = 1); 이 라인을 추가한 이유는 F2, F3과 같이 F회전을 하는 횟수가 정해진 값이 alpha[x]에 들어있는 지 판별하여 그에따른 F회전 횟수를 설정하기 위해 썼습니다.

예를들면 alpha[0]="F2"라면, alpha[0][0]은 F, alpha[0][1]은 2입니다. 즉 alpha[x][1] 값이 존재하는지에 따라 num을 alpha[x][1] 번으로 설정할 지, 아니면 값이 존재하지 않다면 num 을 1로 설정하여 회전을 한번만 실행하도록 할 지 설정했습니다.

---

```Javascript
 for (var i = 0; i < num; i++) {
                var arr2 = [];
                arr2 = this.cubeSplitMoveDR(
                  this.B[2],
                  [this.G[0][0], this.G[1][0], this.G[2][0]],
                  this.R[0],
                  [this.W[0][2], this.W[1][2], this.W[2][2]]
                );
```

일단 arr2 함수 안에 this.cubeSplitMoveDr 메소드 실행 값을 반환받습니다. this.cubeSplitMoveDR에는 F움직임일 때 회전시킬 부분들을 집어넣었습니다.

```Javascript
                this.B[2] = arr2[0];
                this.G[0][0] = arr2[1][0];
                this.G[1][0] = arr2[1][1];
                this.G[2][0] = arr2[1][2];
                this.R[0] = arr2[2];
                this.W[0][2] = arr2[3][0];
                this.W[1][2] = arr2[3][1];
                this.W[2][2] = arr2[3][2];
```

그 후 arr2에 담긴 값을 각 B,G,R,W 배열에 넣습니다. 이러면 하나의 움직임이 끝납니다.

F'의 경우도 마찬가지입니다.

```Javascript
else if (alpha[x].includes("F'")) {
              //F' F'2 F'3...
              var num;
              alpha[x][2] ? (num = alpha[x][2]) : (num = 1);
              for (var i = 0; i < num; i++) {
                var arr2 = [];
                arr2 = this.cubeSplitMoveUL(
                  .
                  .
                  .
```

alpha[x]값에 F'가 포함되어 있을때 실행시킬 부분입니다.

alpha[x][2] ? (num = alpha[x][2]) : (num = 1); 이부분 역시 위의 F의 경우 처럼 alpha[0]="F'2"일때, alpha[0][0]="F",alpha[0][1]="'"alpha[0][2]="2" 가 됩니다.
즉 회전횟수를 정해주는 숫자가 존재한다면, num에 그 값을 넣고, 존재하지 않는다면 num에 1을 넣어 한번만 회전시킵니다.

---

나머지 회전들은 위의 F, F' 의 과정과 같은 맥락으로 작동합니다.

---

moveCube 의 한 회전이 실행될때마다,

```Javascript
            document.write("<h3>" + alpha[x] + "</h3>" + "<br>" + "<br>");
            this.showCube(this.B, this.W, this.O, this.G, this.Y, this.R);
            document.write("<br>" + "<br>");
```

어떤 회전을 통한 결과인지 보이기 위해 alpha[x]를 위에 출력시키고,
showCube에 변화된 B,W,O,G,Y,R을 넘겨줍니다. 모든 움직임이 끝나면 main 함수로 돌아옵니다.

다시 main함수를 보면,

```Javascript

          elapsed = new Date().getTime() - start;
          document.write("소요된 시간: " + elapsed + "초<br>");
          document.write("조작갯수: " + vocabs.length + "<br>");
          document.write("이용해 주셔서 감사합니다. 뚜뚜뚜.");

```

함수가 실행완료된 시점에서 다시한번 시간을 받아와서 시작한 시간을 뺍니다.
그리고 소요시간과 회전갯수를 출력하고 마무리 멘트까지 출력하며 끝납니다.

---

---

---

감사합니다.
