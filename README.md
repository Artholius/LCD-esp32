
#include <SPI.h>
#include <Wire.h>
#include <Adafruit_GFX.h>
#include <Adafruit_SSD1306.h>

#define SCREEN_WIDTH 128  //Comprimento do Display OLED em Pixels.
#define SCREEN_HEIGHT 32  //Largura do Display OLED em Pixels.

//Declaração para o Display SSD1306 Conectado usando I2C
#define OLED_RESET -1  //Pino de Reset do Diaplay
#define SCREEN_ADDRESS 0x3C
Adafruit_SSD1306 display(SCREEN_WIDTH, SCREEN_HEIGHT, &Wire, OLED_RESET);



void setup() {

  Serial.begin(9600);

  //inicialize o objeto do display
  if (!display.begin(SSD1306_SWITCHCAPVCC, SCREEN_ADDRESS)) {
    Serial.println(F("SSD1306 falha na alocação de memória"));
    for (;;)  // Loop infinito vazio. Trava o programa aqui de propósito. se o display não inicializou, não faz sentido continuar — melhor parar do que rodar com comportamento imprevisível.
      ;
  }


  pinMode(26, INPUT);
  pinMode(25, INPUT);
}






void JAMMEROP() {

  if (digitalRead(25) == HIGH) {


    display.clearDisplay();
    display.display();

    display.setTextSize(2.0);
    display.setTextColor(WHITE);
    display.setCursor(10, 15);
    display.println("Opções");
    display.display();

    delay(2000);
    display.clearDisplay();
    display.display();

    display.setTextSize(0.5);
    display.setTextColor(WHITE);
    display.setCursor(10, 15);
    display.println("WIFI jamming");
    display.println("Bluetooth jamming");
    display.display();
  }
}





void loop() {

  display.clearDisplay();
  display.display();

  while (digitalRead(26) == HIGH) {  //Se o pino D26 do Esp32 estiver ligado, chama a função do JAMMER.


    display.clearDisplay();  //Limpa o buffer do display (apaga todo o conteúdo desenhado na memória). Ttexto continua visível fisicamente na tela até você chamar display.display() novamente.

    display.setTextSize(1.5);             //Define o tamanho do Texto que ira aparecer no Display.
    display.setTextColor(WHITE);          //Define a Cor do Texto.
    display.setCursor(10, 15);            //Define a posição do Cursor.
    display.println("EVIL JAMMING 2.0");  //Primeiro Texto que ira aparecer no Displa.
    display.display();

    delay(5000);  //Delay de 5s (segundos).

    int opcoes = 1;

    display.clearDisplay();
    display.setTextSize(1);
    display.setTextColor(WHITE);
    display.setCursor(10, 15);
    display.println("Escolha as opcoes");
    display.display();

    delay(2500);

    while (opcoes == 1) {

      display.clearDisplay();
      display.setTextSize(0.5);
      display.setTextColor(WHITE);
      display.setCursor(0, 5);
      display.println("WIFI Jamming...");
      display.setCursor(0, 10);
      display.println("Bluetooth Jamming...");
      display.display();


    }
  }





























  delay(5000);             //Delay de 5s (segundos).
  display.clearDisplay();  //Limpa o buffer do display (apaga todo o conteúdo desenhado na memória). Ttexto continua visível fisicamente na tela até você chamar display.display() novamente.
}
