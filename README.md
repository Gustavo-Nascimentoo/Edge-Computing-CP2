# 🍷 Vinheria Agnello — Sistema de Monitoramento Ambiental

## 📖 Sobre o Projeto

O **Vinheria Agnello** é um sistema embarcado desenvolvido em **Arduino** com o objetivo de monitorar variáveis ambientais críticas para a conservação adequada de vinhos em estoque.

A solução realiza o acompanhamento em tempo real de:

- 🌡️ Temperatura
- 💧 Umidade
- 💡 Luminosidade

O sistema foi projetado para auxiliar no controle das condições ideais de armazenamento, prevenindo perdas de qualidade causadas por alterações ambientais que afetam diretamente as propriedades físico-químicas e sensoriais dos vinhos.

O projeto foi desenvolvido utilizando o simulador **Wokwi**, integrando sensores, atuadores e displays para representar um cenário real de monitoramento automatizado em adegas e depósitos especializados.

---

## 🎯 Objetivo da Solução

Garantir que o ambiente de armazenamento permaneça dentro dos padrões ideais para conservação de vinhos, emitindo alertas visuais e sonoros sempre que houver condições inadequadas.

---

## 🍇 Importância do Controle Ambiental

O vinho é um produto altamente sensível às condições do ambiente. Pequenas variações podem comprometer seu envelhecimento, aroma, sabor e integridade.

### 💡 Luminosidade

A exposição excessiva à luz, principalmente raios UV, provoca reações químicas que degradam compostos orgânicos do vinho.

#### Condição ideal

- Ambiente escuro ou com baixa incidência de luz.

---

### 🌡️ Temperatura

Temperaturas elevadas aceleram o envelhecimento do vinho e prejudicam sua estabilidade.

#### Faixa ideal

- Entre **10°C e 15°C**
- Ideal aproximado: **13°C**

Oscilações superiores a **3°C** podem gerar alterações indesejadas no aroma e sabor.

---

### 💧 Umidade

A umidade influencia diretamente a conservação das rolhas de cortiça.

#### Problemas causados

- **Baixa umidade:** ressecamento das rolhas e oxidação do vinho.
- **Alta umidade:** proliferação de fungos e deterioração dos rótulos.

#### Faixa ideal

- Entre **60% e 80%**
- Ideal aproximado: **70%**

---

## 🧠 Funcionalidades do Sistema

✅ Leitura contínua dos sensores ambientais  
✅ Cálculo de média de leituras para maior estabilidade  
✅ Alertas visuais com LEDs  
✅ Alertas sonoros com buzzer  
✅ Exibição de dados em display LCD I2C  
✅ Diagnóstico via monitor serial  
✅ Estrutura modular baseada em requisitos independentes

---

## 🛠️ Tecnologias Utilizadas

- Arduino UNO
- Wokwi Simulator
- Linguagem C/C++
- Sensor DHT11
- Sensor LDR
- Display LCD I2C 16x2
- LEDs
- Buzzer

---

## 🔌 Componentes do Circuito

| Componente | Função |
|---|---|
| DHT11 | Leitura de temperatura e umidade |
| LDR | Leitura de luminosidade |
| LCD I2C 16x2 | Exibição das informações |
| LEDs | Indicação visual de status |
| Buzzer | Alerta sonoro |
| Arduino UNO | Controle principal do sistema |

---

## ⚙️ Dependências

Para compilar o projeto no Arduino IDE, instale as seguintes bibliotecas:

### Bibliotecas necessárias

- `DHT sensor library by Adafruit`
- `LiquidCrystal_I2C`
- `Wire`

---

## 📥 Como Instalar as Dependências

### Arduino IDE

1. Abra a **Arduino IDE**
2. Vá em:

```bash
Sketch → Include Library → Manage Libraries
```

3. Pesquise e instale:

- `DHT sensor library by Adafruit`
- `LiquidCrystal I2C`

---

## ▶️ Como Executar o Projeto

### Método 1 — Simulação no Wokwi

1. Acesse o simulador:

👉 https://wokwi.com/projects/464493906224299009

2. Clique em **Start Simulation**
3. Interaja com os sensores virtuais
4. Observe:
   - LEDs
   - LCD
   - Buzzer
   - Monitor serial

---

### Método 2 — Arduino IDE

#### 1. Clone ou copie o projeto

```bash
git clone <url-do-repositorio>
```

Ou copie manualmente o código `.ino`.

---

#### 2. Abra o arquivo na Arduino IDE

```bash
vinheria-agnello.ino
```

---

#### 3. Instale as bibliotecas necessárias

Conforme explicado anteriormente.

---

#### 4. Conecte o Arduino

Selecione:

```bash
Tools → Board → Arduino UNO
```

E escolha a porta correta.

---

#### 5. Faça o upload

Clique em:

```bash
Upload
```

---

## 🧩 Estrutura do Sistema

O projeto foi desenvolvido de forma modular, onde cada requisito representa uma funcionalidade específica.

### Requisitos implementados

| Requisito | Descrição |
|---|---|
| 1–4 | Monitoramento de luminosidade |
| 5–7 | Controle de temperatura |
| 8–10 | Controle de umidade |
| 11–12 | Exibição de dados no LCD |
| 13 | Diagnóstico via Serial Monitor |

---

## 📊 Estratégia de Estabilização dos Dados

Para evitar leituras incorretas e oscilações bruscas dos sensores, o sistema realiza:

- 5 leituras consecutivas
- cálculo da média aritmética
- atualização periódica dos dados

Essa abordagem reduz ruídos e melhora a confiabilidade do monitoramento.

---

## 🚨 Sistema de Alertas

### LEDs

| Cor | Significado |
|---|---|
| 🟢 Verde | Condição ideal |
| 🟡 Amarelo | Atenção |
| 🔴 Vermelho | Condição crítica |

---

### Buzzer

O buzzer é acionado em situações críticas de:

- temperatura inadequada
- umidade fora da faixa aceitável

---

## 🧪 Desafios Enfrentados

Durante o desenvolvimento, alguns desafios importantes foram superados:

- Integração simultânea de múltiplos sensores e atuadores
- Organização da lógica modular dos requisitos
- Gerenciamento de displays e feedback visual
- Redução de ruídos nas leituras
- Estruturação do circuito virtual no Wokwi

---

## 📸 Demonstração

### 🎥 Vídeo Explicativo

👉 https://youtu.be/QlRcLPogc_Y?si=f9WGAQrT55i0F0sy

---

## 📂 Estrutura Sugerida do Projeto

```bash
📦 vinheria-agnello
 ┣ 📜 README.md
 ┣ 📜 vinheria-agnello.ino
 ┗ 📂 assets
```

---

## 👨‍💻 Integrantes do Grupo

| Nome | RM |
|---|---|
| Gustavo Almeida Lopes do Nascimento | RM 571070 |
| João Gabriel Mosqueti Agra Cunha | RM 572017 |
| Leonardo Teodoro Leitão | RM 569724 |
| Rafael Yuta Nischida | RM 570552 |

---

## 📌 Melhorias Futuras

- Integração com IoT
- Dashboard web em tempo real
- Armazenamento em banco de dados
- Alertas por aplicativo/mobile
- Histórico de medições
- Controle automático de climatização

---

## 📄 Licença

Projeto desenvolvido para fins acadêmicos e educacionais.
