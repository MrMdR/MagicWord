/*
  say the...
  
  --- MAGIC WORD! ---
  
  MagicWord v7.1
  (formally Read-a-Tweet)
  
  Your sparkcore reads Twitter and execute an if/else statement when a matching word has been found!
  (acctually... ThingSpeak reads twitter and gives your spark core a kick to do something...)
  
  Anouska de Graaf
  Mark de Reijer
  Base by ls6 (cheerlights) https://github.com/ls6/spark-core-cheerlights/blob/master/spark-standalone/sparkCheerligts.cpp
  
*/

TCPClient client; 

int ledPin = D7; //LED pin
String responseLine;
String MagicTwitterWord;
unsigned long nextPoll = 0;

void setup() { 
    Serial.begin(9600);  
    pinMode(ledPin, OUTPUT);
    delay(2000);
    connectToTwitter();
}

void connectToTwitter() {
  Serial.println("Connecting to Thingspeak...");
  if (client.connect("api.thingspeak.com", 80)){
    Serial.println("Connected to API...");
    client.println("GET /channels/17847/field/1/last.txt HTTP/1.0"); //vervang hier het nummer door jou cannel nummer
    client.println();
    Serial.println("I'm connected to the channel! WooHoo!");
  }
  else {
    Serial.println("Connection failed.... :( But do no need to cry! Just try again and know that you are beautiful :)");
  }
  responseLine = "";
  MagicTwitterWord = "";
}

void readStatus() {
  Serial.println("Entering readStatus...");
  while (client.available()) {
    Serial.println("Client is available!");
    char ch = client.read(); //ch ontvang 1 letter
    //Serial.println("ch"+ch); // laat deze letter zien in de serial monitor
    MagicTwitterWord += ch; //het woord bouwt tie langzaam op door de nieuwe letter achter de voorgaande te plakken.
    Serial.println("Building the magic word... "+MagicTwitterWord);
  };
  client.stop();
  Serial.println("Client stopped and ended the build.");
  MagicTwitterWord.trim();
  Serial.println("the Magic Twitter Word is: "+MagicTwitterWord);
  if (MagicTwitterWord == "happycookie"){
    Serial.println("executing the matching if/else statement...");
    Serial.println("LED D7 is on!");
    switchLight(49);
  }
  else if (MagicTwitterWord == "sadcookie"){
    Serial.println("executing the matching if/else statement...");
    Serial.println("LED D7 is off!");
    switchLight(50);
  }
  else {
    Serial.println("Didn't find a matching magic word."); //Didn't find the status
   // Serial.println(MagicTwitterWord);
   // Serial.println(MagicTwitterWord.length());
  };
}

void switchLight (int CaseNumber) {
  switch (CaseNumber) {
    case 49:
      digitalWrite(ledPin, HIGH);
      break;
    case 50:
      digitalWrite(ledPin, LOW);
      break;
    default:
      digitalWrite(ledPin, LOW);
  };
}

void loop() {
  if (nextPoll <= millis()) {
    nextPoll = millis()+30000;
    connectToTwitter();
  };
  if (client.available()) {
    char ch = client.read();
    responseLine += ch;
    Serial.print(ch);
    //if end of line found
    if (ch == 10) {
      Serial.println(responseLine.length());
      if (responseLine.length() == 2) {
        readStatus();
      };
      responseLine = "";
    };
  };
  if (Serial.available() > 0) {
    char cmd = Serial.read();
    Serial.print("got: ");
    Serial.println(cmd);
    switchLight(cmd);
  };
}
