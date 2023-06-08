O projeto foi criado na plataforma Tinkercad com o intuito de simular um banco de alimentos na qual apresenta sensores para definir se o alimento será bem conservado no local no qual será inserido. O projeto apresenta um teclado numérico, onde com ele pode ser feito as interações com o sistema no qual se mostra bem intuitivo. As informações que devem ser passadas para o sistema é de conhecimento geral, deixando-o assim ainda mais fácil de entender como funciona o mesmo.


Código utilizado no Projeto:
_______________________________________________________________________________________________________________________________________________________________________________________________________________________
#include <Keypad.h>
#include <LiquidCrystal.h>

const byte linhas = 4; // Número de linhas do teclado numérico
const byte colunas = 4; // Número de colunas do teclado numérico
int contador = 0;
const int Led = A1;

char keys[linhas][colunas] = {
  {'1','2','3','A'},
  {'4','5','6','B'},
  {'7','8','9','C'},
  {'*','0','#','D'}
};

byte pinosLinhas[linhas] = {0, 1, 2, 3}; // Conecte as linhas 0-3 do teclado numérico aos pinos 0-3 do Arduino
byte pinosColunas[colunas] = {4, 5, 6, 7}; // Conecte as colunas 4-7 do teclado numérico aos pinos 4-7 do Arduino

Keypad keypad = Keypad(makeKeymap(keys), pinosLinhas, pinosColunas, linhas, colunas);
LiquidCrystal lcd(13, 12,8, 9, 10, 11); // Conecte os pinos RS, E, D4, D5, D6, D7 do display LCD aos pinos correspondentes do Arduino

//declaração do sensor de Temperatura
const int pinSensor = A0;



void setup() {
  lcd.begin(16, 2); // Configure o número de colunas e linhas do display LCD
  Serial.begin(9600);
  pinMode(Led, OUTPUT);
}

void loop() {
  
  
 
  
//-------------------------------------------------------------//
  //definições iniciais
  
  
  
  //char key = keypad.getKey();
  
  //Sensor térmico
  int sensorValue = analogRead(pinSensor);
  
  
 
  // Convertendo a tensão em graus Celsius
  
  float voltagem = sensorValue * (5.0 / 1023.0);
  float temperatura = (voltagem - 0.5) * 100;
  
  
  
//------------------------------------------------------------//
  
  //começo do dialogo
  
  
  lcd.setCursor(0, 0);
  lcd.print("Qual o alimento"); 
  lcd.setCursor(0, 1);
  lcd.print("sera armazenado? ");
  
  delay(5000);
  
  lcd.clear();
  lcd.setCursor(0, 0);
  lcd.print("1 - Carne");
  
  delay(3000);
  
  lcd.clear();
  lcd.setCursor(0, 0);
  lcd.print("2 - Vegetais");
  
  delay(3000);
  
  lcd.clear();
  lcd.setCursor(0, 0);
  lcd.print("3 - Frutas");
  
  
  char key = keypad.waitForKey();
  lcd.clear();
  lcd.setCursor(0,0);
  lcd.print(key);
  delay(3000);
  
  
//-------------------------------------------------------------//
  
  
  
  //opção 1
  
  	if (key == '1') {
    
      lcd.clear();
      lcd.setCursor(0, 0);
      lcd.print("Alimento: ");
      lcd.setCursor(0, 1);
      lcd.print("Carnes");
      delay(5000);
      lcd.clear();
      lcd.setCursor(0, 0);
      lcd.print("O alimento deve");
      lcd.setCursor(0, 1);
      lcd.print("manter-se a -18C");
      delay(5000);    	

      while (temperatura > -18){

          lcd.clear();
          lcd.setCursor(0, 0);
          lcd.print("Diminua sua temp ");
          lcd.setCursor(0, 1);

			digitalWrite(Led, HIGH);
          //Sensor térmico

          int sensorValue = analogRead(pinSensor);
          float voltagem = sensorValue * (5.0 / 1023.0);
          float temperatura = (voltagem - 0.5) * 100;
          lcd.print(temperatura);
          delay(2000);

          if (temperatura < -18){
              lcd.clear();
              lcd.setCursor(0, 0);
              lcd.print("Temp ideal! ");
              lcd.setCursor(0, 1);
              lcd.print(temperatura);
			
            	digitalWrite(Led, LOW);
              delay(5000); 

              lcd.clear();
              lcd.setCursor(0, 0);
              lcd.print("ficara 12 meses");
              lcd.setCursor(0, 1);
              lcd.print("conservado");
              delay(5000);
              break;
            }
          }       
        }

  
  
//-----------------------------------------------------------//
  
  //opção 2
  
  
  
  else if( key == '2'){
  	lcd.clear();
    lcd.setCursor(0, 0);
    lcd.print("Alimento: ");
    lcd.setCursor(0, 1);
    lcd.print("Vegetais");
    delay(5000);
    lcd.clear();
    lcd.setCursor(0, 0);
    lcd.print("Pode congelar?");
    lcd.setCursor(0, 1);
   	lcd.print("S - 1  N - 2");
    char key1 = keypad.waitForKey();
      
      
    delay(3000);
      
    					
      if (key1 == '1'){
		lcd.clear();
        lcd.setCursor(0, 0);
        lcd.print("O alimento deve");
        lcd.setCursor(0, 1);
        lcd.print("manter-se a -18C");
        delay(5000);
          	
        while (temperatura > -18){
            
          	lcd.clear();
            lcd.setCursor(0, 0);
            lcd.print("Diminua sua temp ");
            lcd.setCursor(0, 1);
            digitalWrite(Led, HIGH);
          	//Sensor térmico
          	int sensorValue = analogRead(pinSensor);
            float voltagem = sensorValue * (5.0 / 1023.0);
            float temperatura = (voltagem - 0.5) * 100;
            lcd.print(temperatura);
            
          	delay(2000);
         
          	if (temperatura < -18){
              lcd.clear();
              lcd.setCursor(0, 0);
              lcd.print("Temp ideal! ");
              lcd.setCursor(0, 1);
              lcd.print(temperatura);
				digitalWrite(Led, LOW);
              delay(5000); 

              lcd.clear();
              lcd.setCursor(0, 0);
              lcd.print("ficara 12 meses");
              lcd.setCursor(0, 1);
              lcd.print("conservado");
              delay(5000);
              break;
        }
        	}
        		}
        			
            
        else if(key1 == '2'){
  		lcd.clear();
        lcd.setCursor(0, 0);
        lcd.print("O alimento deve");
        lcd.setCursor(0, 1);
        lcd.print("manter-se a 10C");
        
        delay(5000);
    	
        lcd.clear();
    	lcd.setCursor(0,0);
    	lcd.print("Sua temp atual:");
        lcd.setCursor(0,1);
        
        //Sensor térmico
        
        int sensorValue = analogRead(pinSensor);
        float voltagem = sensorValue * (5.0 / 1023.0);
        float temperatura = (voltagem - 0.5) * 100;
    
    	lcd.print(temperatura);
        delay(3000);
          while (temperatura > 10 || temperatura < 5){  
            lcd.clear();
            lcd.setCursor(0,0);
            lcd.print("Coloque o vegetal");
            lcd.setCursor(0,1);
            lcd.print("entre 5 e 10C");
            digitalWrite(Led, HIGH);
            delay(2000);
            
            //Sensor térmico
        
        	int sensorValue = analogRead(pinSensor);
        	float voltagem = sensorValue * (5.0 / 1023.0);
        	float temperatura = (voltagem - 0.5) * 100;
            
            if (temperatura < 10 && temperatura >= 5){
            	lcd.clear();
            	lcd.setCursor(0,0);
            	lcd.print("O vegetal esta");
            	lcd.setCursor(0,1);
           	 	lcd.print("na temp ideal");
              	digitalWrite(Led, LOW);
              	delay(5000);
              	lcd.clear();
            	lcd.setCursor(0,0);
            	lcd.print("Ficara 7 dias");
            	lcd.setCursor(0,1);
           	 	lcd.print("conservado");
              	delay(5000);
              	break;
              	
            
            }
          		}
        			}}	
          
          
    
    
    
   
  
//-------------------------------------------------------------// 
  
  
  //opção 3
  
  else if( key == '3'){
  	lcd.clear();
    lcd.setCursor(0, 0);
    lcd.print("Alimento: ");
    lcd.setCursor(0, 1);
    lcd.print("Frutas");
    delay(5000);
      lcd.clear();
      lcd.setCursor(0, 0);
      lcd.print("Pode congelar?");
      lcd.setCursor(0, 1);
      lcd.print("S - 1  N - 2");
      char key1 = keypad.waitForKey();
      
      
      delay(3000);
      
    					
      if (key1 == '1'){
		lcd.clear();
        lcd.setCursor(0, 0);
        lcd.print("O alimento deve");
        lcd.setCursor(0, 1);
        lcd.print("manter-se a -18C");
        delay(5000);
          	
        while (temperatura > -18){
            
          	lcd.clear();
            lcd.setCursor(0, 0);
            lcd.print("Diminua sua temp ");
          	digitalWrite(Led, HIGH);
            lcd.setCursor(0, 1);
            
          	//Sensor térmico
          	int sensorValue = analogRead(pinSensor);
            float voltagem = sensorValue * (5.0 / 1023.0);
            float temperatura = (voltagem - 0.5) * 100;
            lcd.print(temperatura);
            
          	delay(2000);
         
          	if (temperatura < -18){
              lcd.clear();
              lcd.setCursor(0, 0);
              lcd.print("Temp ideal! ");
              digitalWrite(Led, LOW);
              lcd.setCursor(0, 1);
              lcd.print(temperatura);

              delay(5000); 

              lcd.clear();
              lcd.setCursor(0, 0);
              lcd.print("Ficara 12 meses");
              lcd.setCursor(0, 1);
              lcd.print("conservado");
              delay(5000);
              break;
        }
        	}
        		}
        			
            
        else if(key1 == '2'){
  		lcd.clear();
        lcd.setCursor(0, 0);
        lcd.print("O alimento deve");
        lcd.setCursor(0, 1);
        lcd.print("manter-se a 10C");
        
        delay(5000);
    	
        lcd.clear();
    	lcd.setCursor(0,0);
    	lcd.print("Sua temp atual:");
        lcd.setCursor(0,1);
        
        //Sensor térmico
        
        int sensorValue = analogRead(pinSensor);
        float voltagem = sensorValue * (5.0 / 1023.0);
        float temperatura = (voltagem - 0.5) * 100;
    
    	lcd.print(temperatura);
        delay(3000);
          while (temperatura > 10 || temperatura < 5){  
            lcd.clear();
            lcd.setCursor(0,0);
            lcd.print("Coloque a fruta");
            lcd.setCursor(0,1);
            lcd.print("entre 5 e 10C");
            digitalWrite(Led, HIGH);
            delay(2000);
            
            //Sensor térmico
        
        	int sensorValue = analogRead(pinSensor);
        	float voltagem = sensorValue * (5.0 / 1023.0);
        	float temperatura = (voltagem - 0.5) * 100;
            
            if (temperatura < 10 && temperatura >= 5){
            	lcd.clear();
            	lcd.setCursor(0,0);
            	lcd.print("A fruta esta");
            	lcd.setCursor(0,1);
           	 	lcd.print("na temp ideal");
              	digitalWrite(Led, LOW);
              	delay(5000);
              	lcd.clear();
            	lcd.setCursor(0,0);
            	lcd.print("ficara 7 dias");
            	lcd.setCursor(0,1);
           	 	lcd.print("conservado");
              	delay(5000);
              	break;
  
  
            
            
  					
          
          
 				}
        
  		
    		}
  	
  		}
  
  	}
  		lcd.clear();
  		lcd.setCursor(0,0);
  		lcd.print("Gostaria de ver o");
  		lcd.setCursor(0,1);
  		lcd.print("item armazenado?");
  		delay(5000);
  		lcd.clear();
  		lcd.setCursor(0,0);
  		lcd.print("1 - S   2 - N");
  		char key3 = keypad.waitForKey();
  		if (key3 == '1'){
          lcd.clear();
          lcd.setCursor(4,0);
          lcd.print("Alimento");
          lcd.setCursor(3,1);
          lcd.print("Armazenado:");
          delay(5000);
          if (key3 == '1'){
              lcd.clear();
              lcd.setCursor(5,0);
              lcd.print("Carne");
              lcd.setCursor(3,1);
              lcd.print("Armazenada");}
          else if(key == '2'){
              lcd.clear();
              lcd.setCursor(5,0);
              lcd.print("Vegetal");
              lcd.setCursor(3,1);
              lcd.print("Armazenado");}	
          else if (key == '3'){
              lcd.clear();
              lcd.setCursor(5,0);
              lcd.print("Fruta");
              lcd.setCursor(3,1);
              lcd.print("Armazenada");}
          delay(5000);}
}
    
  
  

