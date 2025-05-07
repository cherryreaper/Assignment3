# Assignment3

[p5js file](https://editor.p5js.org/cherryreaper/sketches/n6rLP-xm2)

## Explination
I was exploring color and it's movement across the page, as well as the tempo of B&W to color shifting. I realized what I learned in my last assignment in generating triangles to move the colors up the page to generate a roaming ombre effect that looked like TV static when without color.

If I were working on this composiiton more, I would like to hook it up to a heartrate if possible.

## Code


```
//variables
let colorArrayA = [];
let colorArrayB = [];
let triArray = [];
reflection = true;
current_color = 250;
let color1;
let color2;
let color3;
let timer = 0;
let flip = true;
let iteration = 1;

function setup() {
  createCanvas(400, 400);
  rect(0, 0, 400, 400);
  color1 = random(250);
  color2 = random(250);
  color3 = random(250);
  frameRate(20);

  //create pallete
  generatePallete();
}

function draw() {
  //reset
  let x1 = -10,
    y1 = 20;
  let x2 = 0,
    y2 = 0;
  let x3 = 10,
    y3 = 20;
  let reflection = true;

  //loooop
  for (let i = 0; i < 20; i += 1) {
    for (let j = 0; j < 41; j += 1) {
      if (timer < 500) {
        fill(colorArrayA[i][j]); //, colorArrayB[i][j], color3);
        stroke(colorArrayA[i][j]); //, colorArrayB[i][j], color3);
      }
      else{
        fill(colorArrayA[i][j], colorArrayB[i][j], color3);
        stroke(colorArrayA[i][j], colorArrayB[i][j], color3);
        print(timer)
        if (timer > 550 && frameCount < 300){
        timer = 0;
        }
        else if (timer > 600  && frameCount > 300 && frameCount < 600){
        timer = 0;
        }
        else if (frameCount > 1600){
          timer = 0
        }
      }
      triangle(x1, y1, x2, y2, x3, y3);

      x1 = x2;
      y1 = y2;
      x2 = x3;
      y2 = y3;
      if (reflection) {
        y3 = y3 - 20;
        reflection = false;
      } else {
        y3 = y3 + 20;
        reflection = true;
      }
      x3 = x3 + 10;
      current_color = current_color - 0.29;
      fill(255, 255, 0);
    }
    shiftColor();
    //reset
    x1 = -10;
    x2 = 0;
    x3 = 10;
    y1 = y1 + 20;
    y2 = y2 + 20;
    y3 = y3 + 20;
    timer++;
  }
}

function generatePallete() {
  for (let i = 0; i < 20; i += 1) {
    colorArrayA[i] = [];
    colorArrayB[i] = [];
    for (let j = 0; j < 41; j += 1) {
      colorArrayA[i][j] = color1;
      colorArrayB[i][j] = color2;
      if (color1 > 125) {
        color1 = color1 - 10;
      }
      color1 = color1 + random(-10, 10);
      color2 = color2 + random(-10, 10);
    }
  }
}

// Shift colors up
function shiftColor() {
  for (let i = 0; i < 20; i++) {
    for (let j = 0; j < 41; j++) {
      if (i == 0 && j == 0) {
        firstColorA = colorArrayA[i][j];
        firstColorB = colorArrayB[i][j];
      }
      if (i == 19 && j == 40) {
        colorArrayA[i][j] = firstColorA;
        colorArrayB[i][j] = firstColorB;
      } else if (j != 40) {
        colorArrayA[i][j] = colorArrayA[i][j + 1];
        colorArrayB[i][j] = colorArrayB[i][j + 1];
      } else if (j == 40) {
        colorArrayA[i][40] = colorArrayA[i + 1][0];
        colorArrayB[i][40] = colorArrayB[i + 1][0];
      }
    }
  }
}
```
