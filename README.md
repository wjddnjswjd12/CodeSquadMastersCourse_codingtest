# CodeSquadMastersCourse_codingtest

## 코드스쿼드 마스터즈 코스 코딩테스트2

cube 라는 객체 생성 후

1. initialCube에 맨 위에 미리보기로 띄울 값을 넣었습니다.

```Javascript
script>
      var cube = {
        initialCube: [
          ["R", "R", "W"],
          ["G", "C", "W"],
          ["G", "B", "B"],
        ],
        arr2: [
          ["R", "R", "W"],
          ["G", "C", "W"],
          ["G", "B", "B"],
        ],
```

2. 그 후 직접적으로 변화를 줄 arr2라는 객체에 initialCube와 같은 값들을 넣었습니다.

3. cube.word 에 prompt 로 입력을 받고, wordSplit 이라는 메소드로 하나씩 분리했습니다.
   예를들면 ("U'BL'"=>["U'","B","L"]) 이런식으로 했습니다.

4. word.Split메소드의 매개변수로 문자열을 받아와서 var temp에 split("")함수를 통해 하나씩 쪼개고, ' 가 아닌 값이면서(즉 알파벳) 뒤에 '를 가진 (U') 값이면 splice함수로 그 둘을 빼내와서 temp2에 담았습니다.

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

그 후 미리 만들어둔 array배열에 하나씩 push 했습니다.

else if 부분도 비슷한 맥락으로 temp[i]가 ' 가 아닌 값이면서 뒤에도 ' 가 아니면, 즉 그 자신도 알파벳이면서 뒤에 값도 알파벳이라면 자기자신만 splice로 빼와서 push 하도록 설정했습니다.

그리고 splice 하면 temp.length 가 자연스럽게 줄어드니까 이 부분을 while문을 통해 length 가 0이 될때까지 반복시켰습니다.

5. movecube 메소드는 wordSplit메소드로 인해 분리된 배열을 받아와서 for 문을 통해 값이 어떤 알파벳을 담고있는지 판별한다.
   판별되면 orderUpLeft 나 orderDownRight 메소드에 이동시킬 배열을 입력한다.

95번줄의 this.showCube(alpha[i],this.arr2)는 해당 움직임의 알파벳과 큐브를 showCube메소드를 통해 화면에 출력했습니다.

6. orderUpLeft는 위로 한칸씩 이동하거나 왼쪽으로 한칸씩 이동하는 배열들에 적용시키는 메소드입니다. temp라는 변수에 받아온 배열의 맨 앞 값을 받고, 그 받은 값을 push로 밀어넣습니다.

```Javascript
        orderUpLeft: function (array) {
          var temp = array.shift();
          array.push(temp);
          return array;
        },
        orderDownRight: function (array) {
          var temp = array.pop();
          array.unshift(temp);
          return array;
        },

```

orderDownRight 는 아래로, 오른쪽으로 한칸씩 이동하는 배열들에 적용시키는 메소드입니다. pop()으로 맨 뒤 값을 temp에 넣고 unshift로 temp값을 맨 앞에 집어넣습니다.

7. cube.main은 모든것을 제어하는 메소드입니다.

```Javascript
cube.main = function () {
 var value = this.wordSplit(this.word);//값 받아오기
        this.showCube(false, this.initialCube);//아래에 설명
        document.write("CUBE> " + this.word + "<br>");
        if (this.word === "Q") document.write("Bye~");//Q입력시 Bye~
        else if (value) {
          this.movecube(value);
        }
        console.log(value);
      };
      cube.main();//함수 실행

```

this.ShowCube(false,this.initialCube)에 false값을 준 이유는

function showCube(wow,array)에 wow가 true면, 즉 wow가 값을 가지고 있으면 (U,U',R,R',L..등등) 해당 움직임의 알파벳이 뜨도록 설정했습니다. 맨 위에 띄울 큐브에는 알파벳이 필요없기에 false를 입력하여 아무것도 안뜨도록 설정했습니다.
