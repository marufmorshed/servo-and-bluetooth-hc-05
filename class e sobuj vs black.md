int leftir=A2;
int rightir=A0;

const int vspeed=70;
const int turnspeed=70l;
const int turndelay=10;

  const int motorA1      = 3;  
  const int motorA2      = 4; 
  const int motorAspeed  = 2;
  const int motorB1      = 9; 
  const int motorB2      = 10; 
  const int motorBspeed  =11;

int digitalrdright() {
  int ri;
  int x=analogRead(rightir);
  if(x>500) {
  ri=0;
} else {
  ri=1;
} Serial.print("ri");
Serial.println(ri);
return ri;
}

int digitalrdleft() {
  int li;
  int y=analogRead(leftir);
  if(y>400) {
  li=0;
} else {
  li=1;
} 
Serial.print("li");
Serial.println(li);
return li;
}

void lmb() {
  digitalWrite(motorA1,HIGH);
digitalWrite(motorA2,LOW);
analogWrite(motorAspeed, 255);
}
void lmf() {
  digitalWrite(motorA1,LOW);
digitalWrite(motorA2,HIGH);
analogWrite(motorAspeed, 255);
}

void rmf() {
  digitalWrite(motorB1,HIGH);
  digitalWrite(motorB2,LOW);
  analogWrite(motorBspeed, 255);
}

void rmb() {
  digitalWrite(motorB1,LOW);
digitalWrite(motorB2,HIGH);
analogWrite(motorBspeed, 255);
}

void forward() {
  digitalWrite(motorA1,LOW);//lmf
  digitalWrite(motorA2,HIGH);
  analogWrite(motorAspeed, vspeed);
  digitalWrite(motorB1,HIGH);//rmf
  digitalWrite(motorB2,LOW);
  analogWrite(motorBspeed, vspeed);
  Serial.println("forward");
}
void backward() {
  digitalWrite(motorA1,HIGH);//lmb
  digitalWrite(motorA2,LOW);
  analogWrite(motorAspeed, vspeed);
  digitalWrite(motorB1,LOW);
  digitalWrite(motorB2,HIGH);
  analogWrite(motorBspeed, vspeed);
  Serial.println("Backward");
  
}


void turnright() {
  digitalWrite(motorA1,LOW);//lmf
  digitalWrite(motorA2,HIGH);
  analogWrite(motorAspeed, turnspeed);
  digitalWrite(motorB1,LOW);
  digitalWrite(motorB2,HIGH);
  analogWrite(motorBspeed, 0);
  Serial.println("turnright");
}

void turnleft() {
  digitalWrite(motorB1,HIGH);
  digitalWrite(motorB2,LOW);
  analogWrite(motorBspeed, turnspeed);
  digitalWrite(motorA1,HIGH);
  digitalWrite(motorA2,LOW);
  analogWrite(motorAspeed, 0);
  Serial.println("turnleft");
}void mstop() {
  digitalWrite(motorB1,LOW);
  digitalWrite(motorB2,LOW);
  analogWrite(motorBspeed, 0);
  digitalWrite(motorA1,LOW);
  digitalWrite(motorA2,LOW);
  analogWrite(motorAspeed, 0);
  Serial.println("mstop");
}
void setup() {
   pinMode(A0, INPUT);
   pinMode(A2, INPUT);
   pinMode(2,OUTPUT);
   pinMode(3,OUTPUT);
   pinMode(4,OUTPUT);
   pinMode(9,OUTPUT);
   pinMode(10,OUTPUT);
   pinMode(11,OUTPUT);
  
  Serial.begin(9600);
  
  // put your setup code here, to run once:

}

void loop() {
  
 /* int ri,li;
ri=digitalrdright();
li=digitalrdleft();


Serial.print("ri=");
Serial.println(ri);
Serial.print("li=");
Serial.println(li);

delay(1000);*/
int ris=digitalrdright();
int lis=digitalrdleft();
if(ris==1 && lis==0) {
  turnright();
}
if(ris==0 && lis==1) {
  turnleft();
}
if (ris==0 && lis==0) {
  forward();
}
if (ris==1 && lis==1) {
  mstop();
}
  
  // put your main code here, to run repeatedly:

}
