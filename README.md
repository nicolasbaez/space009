## : : s p a c e 0 0 9

![space](https://github.com/nicolasbaez/space009/blob/master/space009.gif)

```processing
int cantidad=96;
float vertices=3;
float ancho=0.3;
float angulo[]=new float[cantidad];
float radio[]=new float[cantidad];
float vx[]=new float[cantidad];
float kx[]=new float[cantidad];
float rr[]=new float[cantidad];
float gg[]=new float[cantidad];
float bb[]=new float[cantidad];
float xx;
float yy;
float zz;
float xRot=0;
float yRot=0;
float zRot=0;
int cuadros=0;
void setup() {
  size(512, 256, P3D);
  for (int i=0; i<cantidad; i++) {
    vx[i]=random(2)+1;
    kx[i]=0;
    rr[i]=random(0);
    gg[i]=random(255);
    bb[i]=random(255);
  }
}
void draw() {
  background(0);
  translate(width/2, height/2, 0);
  rotateX(radians(xRot));
  rotateY(radians(yRot));
  rotateZ(radians(zRot));
  for (int i=0; i<cantidad; i++) {
    radio[i]=map(sin(radians(map(i, 0, cantidad, 0, 180))), 0, 1, height*0.05, height*ancho);
    zz=map(i, 0, cantidad, -height*ancho, height*ancho);
    noFill();
    stroke(rr[i], gg[i], bb[i], map(sin(radians(map(xRot, 0, 360, 0, 180))), 0, 1, 0, 255));
    beginShape();
    for (int j=int(kx[i]); j<=360+kx[i]; j+=360/vertices) {
      xx=radio[i]*cos(radians(j));
      yy=radio[i]*sin(radians(j));
      vertex(xx, yy, zz);
    }
    endShape();
    kx[i]+=vx[i];
  }
  xRot+=0.5;
  if (xRot<=360) {
    saveFrame("gif/space009-######.png");
  }
}
```
