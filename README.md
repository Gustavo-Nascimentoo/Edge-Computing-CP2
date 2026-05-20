## 👥 Integrantes do Grupo
 * *Gustavo Almeida Lopes do Nascimento* — RM 571070
 * *João Gabriel Mosqueti Agra Cunha* — RM 572017
 * *Leonardo Teodoro Leitão* — RM 569724
 * *Rafael Yuta Nischida* — RM 570552
 
 # # Vinheria Agnello - Sistema de Monitoramento Ambiental 🍷
Este projeto consiste em um sistema automatizado de monitoramento de *luminosidade, temperatura e umidade* desenvolvido para a *Vinheria Agnello*. O objetivo principal é garantir a integridade e a máxima qualidade dos vinhos armazenados em estoque, protegendo-os de fatores climáticos que possam degradar suas propriedades organolépticas.
## 📋 Contextualização e Importância do Problema
O vinho é um produto extremamente complexo e sensível, considerado por muitos uma bebida "viva". Pequenas flutuações nas condições do ambiente podem alterar permanentemente seu sabor, aroma e longevidade. O sistema monitora três inimigos silenciosos do vinho:
 1. *Luminosidade:* A exposição à luz forte (especialmente raios UV) inicia reações químicas que alteram os compostos orgânicos da bebida, estragando seu sabor. O ideal é manter o ambiente em penumbra constante.
 2. *Temperatura:* O calor excessivo acelera o envelhecimento precoce do vinho. Além disso, oscilações térmicas de mais de 3^\circ\text{C} causam o aparecimento de aromas indesejados. A temperatura ideal de conservação gira em torno de *13^\circ\text{C}*.
 3. *Umidade:* O ar muito seco (umidade baixa) resseca as rolhas de cortiça, permitindo a entrada de oxigênio que oxida o vinho. Por outro lado, o excesso de umidade destrói os rótulos e estimula a proliferação de fungos e mofo. O nível ideal deve ser mantido próximo a *70%* (com variação aceitável entre 60% e 80%).
## 🛠️ Desafios Superados na Solução
Durante o desenvolvimento do protótipo no simulador *Wokwi*, o grupo enfrentou e superou desafios cruciais de engenharia:
 * *Complexidade da Montagem:* Integrar múltiplos componentes físicos (atuadores sonoros, barras de LEDs e telas) para responder a 3 variáveis simultâneas exigiu um planejamento rigoroso no mapeamento e organização da fiação virtual.
 * *Interface Clara com 3 Displays:* Para que o usuário do depósito compreendesse os dados sem confusão, estruturamos uma lógica visual clara para o isolamento de cada métrica (temperatura, umidade e luz), evitando a poluição de dados em uma única tela.
 * *Estabilidade dos Dados:* Implementamos uma rotina de software para calcular a *média de 5 leituras consecutivas* antes de atualizar os valores a cada 5 segundos. Isso elimina picos falsos e leituras erráticas causadas por ruídos nos sensores.

## 💻 Código-Fonte do Projeto

O código abaixo foi implementado em ambiente Arduino para gerenciar:

- leitura dos sensores DHT11 e LDR
- cálculo de médias aritméticas
- controle de LEDs e buzzer
- exibição de dados no LCD
- monitoramento modular por requisitos

```cpp
#include <Wire.h>
#include <LiquidCrystal_I2C.h>
#include <DHT.h>

// ====================
// DEFINIÇÕES DE PINOS
// ====================

#define DHTPIN 6
#define DHTTYPE DHT11

#define LDR A0

#define LED_VERDE 2
#define LED_AMARELO 3
#define LED_VERMELHO 4

#define BUZZER 5

// ====================
// OBJETOS
// ====================

LiquidCrystal_I2C lcd(0x27, 16, 2);
DHT dht(DHTPIN, DHTTYPE);

// ====================
// VARIÁVEIS GLOBAIS
// ====================

float temperatura;
float umidade;
int luminosidade;

// ====================
// SETUP
// ====================

void setup() {

  pinMode(LED_VERDE, OUTPUT);
  pinMode(LED_AMARELO, OUTPUT);
  pinMode(LED_VERMELHO, OUTPUT);
  pinMode(BUZZER, OUTPUT);

  lcd.init();
  lcd.backlight();

  dht.begin();

  Serial.begin(9600);
}

// ====================
// LOOP PRINCIPAL
// ====================

void loop() {

  lerSensores();

  // CHAME APENAS OS REQUISITOS NECESSÁRIOS

  // requisito1();
  // requisito2();
  // requisito3();
  // ...

  delay(1000);
}

// ====================
// LEITURA DOS SENSORES
// ====================

void lerSensores() {

  float somaTemp = 0;
  float somaUmid = 0;
  int somaLuz = 0;

  for (int i = 0; i < 5; i++) {

    somaTemp += dht.readTemperature();
    somaUmid += dht.readHumidity();
    somaLuz += analogRead(LDR);

    delay(100);
  }

  temperatura = somaTemp / 5;
  umidade = somaUmid / 5;
  luminosidade = somaLuz / 5;
}

// ====================
// FUNÇÕES AUXILIARES
// ====================

void desligarTudo() {

  digitalWrite(LED_VERDE, LOW);
  digitalWrite(LED_AMARELO, LOW);
  digitalWrite(LED_VERMELHO, LOW);

  digitalWrite(BUZZER, LOW);
}

void limparLCD() {

  lcd.clear();
  lcd.setCursor(0, 0);
}

void mostrarValor(String texto, float valor, String unidade) {

  lcd.clear();

  lcd.setCursor(0, 0);
  lcd.print(texto);

  lcd.setCursor(0, 1);
  lcd.print(valor);
  lcd.print(unidade);
}

// ====================
// REQUISITOS DE LUMINOSIDADE
// ====================

void requisito1() {

  if (luminosidade < 400) {
    digitalWrite(LED_VERDE, HIGH);
  }
}

void requisito2() {

  if (luminosidade >= 400 && luminosidade < 700) {
    digitalWrite(LED_AMARELO, HIGH);
  }
}

void requisito3() {

  if (luminosidade >= 700) {
    digitalWrite(LED_VERMELHO, HIGH);
  }
}

void requisito4() {

  limparLCD();

  if (luminosidade < 400) {
    lcd.print("Escuro");
  }
  else if (luminosidade < 700) {
    lcd.print("Meia Luz");
  }
  else {
    lcd.print("Muito Claro");
  }
}

// ====================
// REQUISITOS DE TEMPERATURA
// ====================

void requisito5() {

  if (temperatura >= 10 && temperatura <= 15) {

    digitalWrite(LED_VERDE, HIGH);

    lcd.clear();

    lcd.setCursor(0, 0);
    lcd.print("Temp Ideal");

    lcd.setCursor(0, 1);
    lcd.print(temperatura);
    lcd.print((char)223);
    lcd.print("C");
  }
}

void requisito6() {

  if (temperatura > 15) {

    digitalWrite(LED_AMARELO, HIGH);

    tone(BUZZER, 1000);

    lcd.clear();

    lcd.setCursor(0, 0);
    lcd.print("Temp Alta");

    lcd.setCursor(0, 1);
    lcd.print(temperatura);
    lcd.print((char)223);
    lcd.print("C");
  }
}

void requisito7() {

  if (temperatura < 10) {

    digitalWrite(LED_AMARELO, HIGH);

    tone(BUZZER, 1000);

    lcd.clear();

    lcd.setCursor(0, 0);
    lcd.print("Temp Baixa");

    lcd.setCursor(0, 1);
    lcd.print(temperatura);
    lcd.print((char)223);
    lcd.print("C");
  }
}

// ====================
// REQUISITOS DE UMIDADE
// ====================

void requisito8() {

  if (umidade >= 50 && umidade <= 70) {

    digitalWrite(LED_VERDE, HIGH);

    lcd.clear();

    lcd.setCursor(0, 0);
    lcd.print("Umidade OK");

    lcd.setCursor(0, 1);
    lcd.print(umidade);
    lcd.print("%");
  }
}

void requisito9() {

  if (umidade > 70) {

    digitalWrite(LED_VERMELHO, HIGH);

    tone(BUZZER, 1000);

    lcd.clear();

    lcd.setCursor(0, 0);
    lcd.print("Umidade Alta");

    lcd.setCursor(0, 1);
    lcd.print(umidade);
    lcd.print("%");
  }
}

void requisito10() {

  if (umidade < 50) {

    digitalWrite(LED_VERMELHO, HIGH);

    tone(BUZZER, 1000);

    lcd.clear();

    lcd.setCursor(0, 0);
    lcd.print("Umidade Baixa");

    lcd.setCursor(0, 1);
    lcd.print(umidade);
    lcd.print("%");
  }
}

// ====================
// EXIBIÇÃO E DIAGNÓSTICO
// ====================

void requisito11() {

  mostrarValor("Temperatura", temperatura, "C");
}

void requisito12() {

  mostrarValor("Umidade", umidade, "%");
}

void requisito13() {

  Serial.print("Temp: ");
  Serial.print(temperatura);

  Serial.print(" | Umidade: ");
  Serial.print(umidade);

  Serial.print(" | Luz: ");
  Serial.println(luminosidade);
}
```

### 🌐 Links do Projeto
 * *Simulador do Circuito (Wokwi): 

https://wokwi.com/projects/464493906224299009

 * *Vídeo Explicativo do Youtube/Loom:

https://youtu.be/QlRcLPogc_Y?si=f9WGAQrT55i0F0sy
