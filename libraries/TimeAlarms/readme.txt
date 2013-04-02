#include <Servo.h>

#include <Time.h>

#include <TimeAlarms.h>




Servo servo1;
int pos=0;

void setup()
{
 Serial.begin(9600);
 servo1.attach(9); 
 servo1.write(0);
 setTime(10,45,0,11,20,12);
 Alarm.alarmRepeat(10,44,0,feedFish);
 Alarm.timerOnce(4, feedFish);
}

void loop(){
 Alarm.delay(1000);
  // feedFish(); 
}


void feedFish(){
 Serial.write("feed fish");
  for(pos = 0;pos<180; pos+=1){
    servo1.write(pos);
     delay(15); 
  }
  
  shake();
  shake();
  shake();
  
  for(pos = 180;pos>=1; pos-=1){
    servo1.write(pos);
     delay(15); 
  } 
   
   
}

void shake(){
  int tgt = 100;
  for(pos = 180;pos<tgt; pos-=1){
     servo1.write(pos);
     delay(5); 
  }
  
   for(pos = tgt ;pos<180; pos+=1){
     servo1.write(pos);
     delay(5); 
  }
}
