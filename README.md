컴퓨터 그래픽스 과제
=============
***

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
