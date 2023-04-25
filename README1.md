# RoueDeFortune
#Roue de fortune simple

#Installez Processing en allant sur https://processing.org/download/ et en choisissant la version appropriée pour votre système d'exploitation.
#Ouvrez Processing et créez un nouveau sketch (fichier).
#Copiez et collez le code suivant dans le nouvel sketch :

int numSegments = 8;
float anglePerSegment;
float rotationSpeed = 0;
float currentAngle = 0;
boolean spinning = false;

void setup() {
  size(800, 800);
  anglePerSegment = 360.0 / numSegments;
}

void draw() {
  background(255);
  translate(width / 2, height / 2);
  currentAngle += rotationSpeed;
  
  if (spinning) {
    rotationSpeed = lerp(rotationSpeed, 0, 0.01);
    if (rotationSpeed < 0.01) {
      rotationSpeed = 0;
      spinning = false;
    }
  }
  
  for (int i = 0; i < numSegments; i++) {
    pushMatrix();
    rotate(radians(currentAngle + anglePerSegment * i));
    fill(i % 2 == 0 ? color(255, 0, 0) : color(0, 255, 0));
    arc(0, 0, width * 0.8, height * 0.8, 0, radians(anglePerSegment));
    popMatrix();
  }
  
  stroke(0);
  strokeWeight(3);
  line(0, 0, width * 0.4, 0);
}

void mousePressed() {
  if (!spinning) {
    spinning = true;
    rotationSpeed = random(5, 10);
  }
}
