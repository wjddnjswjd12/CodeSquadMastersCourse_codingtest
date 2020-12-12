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

var start 에 시작시간을 담았습니다. 나중에 끝난 시간은 elapsed 변수에 담았습니다. 그리고

```Javascript
this.showCube(this.B, this.W, this.O, this.G, this.Y, this.R);
```

화면의 맨 윗부분에
