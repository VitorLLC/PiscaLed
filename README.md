// # PiscaLed

#define pinBotao1        2
#define pinBotao2        3


#define pinLEDVerde      8 
#define pinLEDAmarelo    9
#define pinLEDVermelho  10
static byte contador;


class PiscaLed{
    public:
    PiscaLed(byte pinLed, int tempoPisca = 1000);
    void play();
    void stop();
    void loop();
    

    private:
    unsigned long delayPisca;
    bool estadoPisca;
    byte pino;
    int tempo;
  };
PiscaLed::PiscaLed(byte pinLed, int tempoPisca){
  pinMode(pinLed, OUTPUT);
  pino = pinLed;
  tempo = tempoPisca;
  estadoPisca = false;
  }
void PiscaLed::play(){
  estadoPisca = true;
  delayPisca = millis();
}
void PiscaLed::stop(){
  estadoPisca = false;
  digitalWrite(pino, LOW);
}
void PiscaLed::loop(){
  if(estadoPisca){
    if((millis() - delayPisca) < tempo) {
      digitalWrite(pino, LOW);
    }else if ((millis() - delayPisca) < (tempo * 2)) {
      digitalWrite(pino, HIGH);
    }
    else{
      delayPisca = millis();
    }
    }
  else{
    digitalWrite(pino, LOW);
  }
  }

  PiscaLed LedV(pinLEDVerde,     1000);
  PiscaLed LedAm(pinLEDAmarelo,  2000);
  PiscaLed LedVm(pinLEDVermelho, 3000);


 


void setup(){
pinMode(pinBotao1, INPUT_PULLUP); 
pinMode(pinBotao2, INPUT_PULLUP);
}
void loop(){
  LedV.loop();
  LedAm.loop();
  LedVm.loop();
    if(!digitalRead(pinBotao1)){
      LedV.play();
      LedAm.play();
      LedVm.play();
    }
    if(!digitalRead(pinBotao2)){
      LedV.stop();
      LedAm.stop();
      LedVm.stop();     
    }
}
