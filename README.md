컴퓨터 그래픽스 과제
=============
***

-intro-

저희 팀은 모여서 각자 사전에 조사한 것을 바탕으로 프로젝트를 어떻게 진행할지 의논했습니다. 그러고서 다음 사항들을 목표로 잡았습니다. 
<pre><code>
  -목표-
  1. 하늘에 떠있는 달(normalMaterial 사용) 
  2. 낮은 시점으로 지형을 지나가는 느낌주기 
  3. 달의 위상 표현하기
  4. 사용자 주변이 밝아지는 상황만들기
  5. 마우스로 화면을 조작할 수 있게 만들기
</code></pre>

# 1. 코드

<pre><code>

var cols, rows;
var scl = 20;
var w = 1400;
var h = 1000;
let cam;

var flying = 0;

var terrain = [];
function setup() {
createCanvas(600, 600, WEBGL);
cols = w / scl;
rows = h / scl;
cam = createCamera();//카메라 생성
cam.setPosition(0,0,100);//카메라 좌표설정

for (var x = 0; x < cols; x++) {
terrain[x] = [];
for (var y = 0; y < rows; y++) {
terrain[x][y] = 0;
}
}
noStroke();//연결선 제거
}

function draw() {
  let locX = mouseX - width/2;
  let locY = mouseY - height;
  ambientLight(50);//환경광원 설정
  pointLight(255,255,0, 0, -50, 100);//사용자 주변의 지역광원 설정
  cam.lookAt(mouseX-300,(mouseY-200)/3,0);//마우스로 카메라 시점변경
  ellipse( mouseX-300, -87, 35, 35);//구체를 가리는 타원 생성(달의 위상변화 연출)

flying -= 0.01;
var yoff = flying;
for (var y = 0; y < rows; y++) {
var xoff = 0;
for (var x = 0; x < cols; x++) {
terrain[x][y] = map(noise(xoff, yoff), 0, 1, -100, 100);
xoff += 0.5;
}
yoff += 0.2;
}
background(0);
translate(0, 50);
rotateX(PI / 3);
translate(-w / 2, -h / 2);
for (var y = 0; y < rows - 1; y++) {
beginShape(TRIANGLE_STRIP);
for (var x = 0; x < cols; x++) {
let v = terrain[x][y];
v = map(v, -100,100,0,255);
fill(v-64,v-32,v);
vertex(x * scl, y * scl, terrain[x][y]);
vertex(x * scl, (y + 1) * scl, terrain[x][y + 1]);
}
endShape();
}
translate(700,0,200);//구 위치 변경
normalMaterial();//구체에 normalMaterial 적용
sphere(55);//구 생성
}

</code></pre>
***

## 2. 실습

![2](https://user-images.githubusercontent.com/50646883/161415362-96ca52f1-e5c4-48f9-b344-1847cebd7c5b.png)
![3](https://user-images.githubusercontent.com/50646883/161415364-2587eb3b-85a7-4791-aea4-4fb274d814b4.png)
![4](https://user-images.githubusercontent.com/50646883/161415365-8e3d8f21-cfde-4e47-b5bb-896c6d9c99f7.png)
![1](https://user-images.githubusercontent.com/50646883/161415366-d516fd8c-ec1a-4ed5-b030-81c12b054de4.png)

gif
![과제_AdobeCreativeCloudExpress](https://user-images.githubusercontent.com/50646883/161415402-9ebe77d0-6586-4641-81bd-162698256ad6.gif)
gif상에서는 화질이 조금 깨져서 나온다.

***

### 3.소감

박형민 : 
> 3d 지형이라는 어려운 코드를 팀원들과 함께 서로 협동하여 이해해보면서 3d지형에 대한 코드를 조금더 쉽게 이해할 수 있었습니다. Light와 Camera, Material 등을 더 추가로 사용해보면서 > 창의력만 좋다면 더 좋은 프로그램을 만들수 있을것 같다는 생각이 들었습니다. 팀과제를 통해 서로간에 부족한 부분을 보완할 수 있었고 그래픽스 수업에 대한 자신감도 생길수 있었습니다.

김준영 : 
> 2학년 개강이후 첫 팀프로젝트를 하였는데 1학년때와는 다른느낌이였다. 각자 공부해보고 팀프로젝트를 실시하려 하였는데 막상 수업떄는 다 알것같은 그런 느낌이였는데 혼자 공부하려해보니 > 많이 부족한거 같다. 하지만 동기들에게 조언을 구하고 같이 코딩을 해석해보니 조금씩 알아가는것 같았고 팀프로젝트를 하면서 몰랐었던 부분을 알게되었고 조금 성장해 나아간 것 같았다.

지영수 :
> 이번 과제를 하며 마우스를 따라 카메라가 움직이는 동시에 광원도 같이 움직이는 프로그램을 짜고 싶었으나 뜻대로 되지 않아 힘들었던 것 같다. 예제 등을 참고하여 문제를 해결하려 했으나 
>  쉽게 풀리지 않아 답답했고, 여러 함수들을 잘 활용하는 팀원들을 보며 도움이 되지 않는것같아 미안한 마음이 컸다. 이번 팀 과제를 통해 나도 더욱 열심히 공부하여 팀원들처럼 프로그램을 > 잘 짤수 있도록 해야겠다고 느꼈다.

김용환 :
> 팀 프로젝트 과제를 하면서 팀원들에 비해 많이 부족하다는걸 느꼈고 더 도움이 될수 있도록 공부를 많이 해야겠다라는 생각이 들었습니다. light,camera,material을 활용하여 terrain 코드> 를 변형시키면서 어떤식으로 변형이 가능하고 활용될수있는지  알게되었습니다. 어려웠지만 배울점이 많았던 프로젝트였던것 같습니다.

김기찬 :
> 이번 과제를 통해서 p5.js의 함수나 구성에 대해 전문적으로 접근할 수 있는 좋은 기회를 얻은 것 같습니다. 3차원 공간에서의 카메라의 시점관리나 광원의 위치, 방향 등을 고려해 보면서
> 평소에 몇몇 프로그램에서 시점을 편하게 이동시킬 수 있는 것이 직접 생각하여 코딩하면 많이 어려울 수 있다는 것을 느꼈습니다. 그리고 그래픽스를 하며 수학에 대한 필요성을 느끼기 시작
> 하게 되어 지금까지와는 다른 계산적인 프로그래밍을 한다는 느낌을 많이 받았습니다. 이해해가는 과정에서 즐거움을 느낄 수 있었고 자신의 부족한 점도 알 수 있게 된 좋은 경험이었다고 생
> 각합니다.
