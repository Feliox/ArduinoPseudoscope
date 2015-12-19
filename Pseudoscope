//0$ 5 channel Arduino scope (sort-of)
//Coded with <3 by Richard Stefun, 2015

int sensorValue; //Variable for sensor readings
#define stopPin 3 //Scope pause pin - pull high to stop
#define maxSizeDivider 30 //This value will divide the ADC reading for trace representation   << Tune this if traces blend together - 25 is fine for 4 channels @ 1080 screen.
#define scopeTraceFillAsciiChar "*" //Char fill, from left side to trace position
#define scopeTraceAsciiChar "#" //Trace character
#define channelCount 5 //Numbers of channels. Less channels - faster sample rate

void setup() {
  Serial.begin(115200); //Start the fastest serial transmission officialy supported by Arduino IDE
  pinMode(stopPin, INPUT); //set Pause pin as Input
}

void loop() {
  while(digitalRead(stopPin)); //Simple execution "Pause"
  for(int c = 0; c < channelCount; c++){ //Channel sampling loop
    sensorValue = analogRead(c); //ARead current channel
    for(int s = 0; s < ((1023/maxSizeDivider)+20)*c; s++) Serial.print(" "); // Channel padding
    Serial.print(c); //Print channel number
    Serial.print(" - "); //Padding
    Serial.print(sensorValue); //Print analog reading
    Serial.print(" - "); //Padding
    for(int i = 0; i < (sensorValue/maxSizeDivider)-1; i++) Serial.print(scopeTraceFillAsciiChar); //Print trace fill
    Serial.print(scopeTraceAsciiChar); //Print trace
    Serial.print(" - "); //Padding
    Serial.print(millis()); //Print millis, to identify changes
    Serial.println("");  //Terminate line
    //delay(2);    //Uncomment if you want to slow down the scope a bit - this will reduce sample rate     
  }  
}

//Possible improvements - use inline avr c to speed up ADC reading. Speeding up communication.
