#include "DHT.h"

#define DHT_PIN 15
#define LDR_PIN 34
#define BTN_N_PIN 19
#define BTN_P_PIN 18
#define BTN_K_PIN 5
#define RELAY_PIN 23

#define DHT_TYPE DHT22
DHT dht(DHT_PIN, DHT_TYPE);

const float UMIDADE_MINIMA_PARA_IRRIGAR = 60.0;
const float PH_IDEAL_MINIMO = 6.0;
const float PH_IDEAL_MAXIMO = 6.8;

void setup() {
  Serial.begin(115200);
  Serial.println("=========================================");
  Serial.println("  FarmTech Solutions - Iniciando Sistema ");
  Serial.println("=========================================");

  dht.begin();

  pinMode(BTN_N_PIN, INPUT_PULLUP);
  pinMode(BTN_P_PIN, INPUT_PULLUP);
  pinMode(BTN_K_PIN, INPUT_PULLUP);
  pinMode(LDR_PIN, INPUT);
  pinMode(RELAY_PIN, OUTPUT);
  digitalWrite(RELAY_PIN, LOW);
}

void loop() {
  float umidade = dht.readHumidity();
  if (isnan(umidade)) {
    Serial.println("Erro ao ler dados do sensor DHT!");
    return;
  }

  int valorLDR = analogRead(LDR_PIN);
  float ph = map(valorLDR, 0, 4095, 0.0, 14.0);

  bool nivelN_OK = !digitalRead(BTN_N_PIN);
  bool nivelP_OK = !digitalRead(BTN_P_PIN);
  bool nivelK_OK = !digitalRead(BTN_K_PIN);

  Serial.println("\n------------------------------------");
  Serial.print("Leitura em: "); Serial.println(millis());
  Serial.print("  [💧] Umidade do Solo: "); Serial.print(umidade); Serial.println("%");
  Serial.print("  [💡] pH (Simulado): "); Serial.println(ph);
  Serial.print("  [🌱] Nutrientes (N/P/K): ");
  Serial.print(nivelN_OK ? "N OK " : "N Baixo ");
  Serial.print(nivelP_OK ? "P OK " : "P Baixo ");
  Serial.println(nivelK_OK ? "K OK" : "K Baixo");

  bool precisaDeAgua = umidade < UMIDADE_MINIMA_PARA_IRRIGAR;
  bool phEstaIdeal = (ph >= PH_IDEAL_MINIMO && ph <= PH_IDEAL_MAXIMO);
  bool nutrientesEstaoOk = (nivelN_OK && nivelP_OK && nivelK_OK);
  
  Serial.println("--- Avaliando Condicoes ---");
  Serial.print("  - Precisa de agua? "); Serial.println(precisaDeAgua ? "SIM" : "NAO");
  Serial.print("  - pH esta ideal?   "); Serial.println(phEstaIdeal ? "SIM" : "NAO");
  Serial.print("  - Nutrientes OK?   "); Serial.println(nutrientesEstaoOk ? "SIM" : "NAO");

  if (precisaDeAgua && phEstaIdeal && nutrientesEstaoOk) {
    Serial.println("\n>>> RESULTADO: CONDIÇÕES IDEAIS. LIGANDO BOMBA D'ÁGUA.");
    digitalWrite(RELAY_PIN, HIGH);
  } else {
    Serial.println("\n>>> RESULTADO: CONDIÇÕES NÃO ATENDIDAS. BOMBA DESLIGADA.");
    digitalWrite(RELAY_PIN, LOW);
  }

  delay(5000);
}
