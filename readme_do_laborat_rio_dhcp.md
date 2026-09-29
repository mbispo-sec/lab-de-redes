# 🌐 Laboratório de Redes: Implementação e Análise de Servidor DHCP

Projeto prático desenvolvido para simular a alocação dinâmica de endereços IP utilizando o **Cisco Packet Tracer**, além de inspecionar o ciclo de concessão de endereçamento via modo de simulação.

## 📌 Objetivo do Laboratório

* Configurar um servidor dedicado para atuar como servidor DHCP na rede local.

* Conectar múltiplos dispositivos finais (estações de trabalho, laptop e impressora de rede) por meio de um switch de camada 2.

* Validar a obtenção dinâmica de parâmetros de rede (IP, Máscara e Gateway).

* Analisar o fluxo de pacotes do processo de concessão **DORA** (*Discover, Offer, Request, Acknowledge*).

## 🏗️ Topologia da Rede

### Dispositivos Utilizados

* **1x Servidor Dedicado** (`Server-PT`)

* **1x Switch 24 portas** (`Switch 2960` ou `Switch-PT`)

* **3x Desktops** (`PC0`, `PC1`, `PC2`)

* **1x Laptop** (`Laptop0`)

* **1x Impressora de Rede** (`Printer0`)

## 📋 Plano de Endereçamento

| Dispositivo / Parâmetro | Tipo de Configuração | Endereço IP / Faixa | Máscara de Sub-rede | Gateway Padrão | 
 | ----- | ----- | ----- | ----- | ----- | 
| **Servidor DHCP** | Estático | `192.168.1.2` | `255.255.255.0` (/24) | `192.168.1.1` | 
| **Gateway Padrão (Simulado)** | \- | `192.168.1.1` | `255.255.255.0` (/24) | \- | 
| **Pool DHCP (Início)** | Dinâmico | `192.168.1.10` em diante | `255.255.255.0` (/24) | `192.168.1.1` | 
| **Clientes (PCs, Laptop, Impressora)** | DHCP | Concedido dinamicamente | `255.255.255.0` (/24) | `192.168.1.1` | 

## ⚙️ Passo a Passo das Configurações

### 1. Configuração do Servidor

1. No `Server0`, configurou-se um IP estático na interface `FastEthernet0` (`192.168.1.2` com máscara `255.255.255.0`).

2. Acesse a aba **Services** > **DHCP**:

   * Serviço DHCP: **ON**

   * Pool Name: `serverPool`

   * Default Gateway: `192.168.1.1`

   * Start IP Address: `192.168.1.10`

   * Subnet Mask: `255.255.255.0`

   * Maximum number of Users: `50`

   * Clique em **Save**.

### 2. Configuração dos Dispositivos Finais

1. Em cada estação (`PC0`, `PC1`, `PC2`, `Laptop0` e `Printer0`), foi acessada a seção de configuração de IP (`Desktop > IP Configuration`).

2. A opção de configuração foi alterada de **Static** para **DHCP**.

3. Confirmou-se o status *DHCP request successful* com a atribuição correta dos parâmetros de rede.

## 🔍 Análise do Processo DORA (Modo de Simulação)

Utilizando a ferramenta de simulação do Packet Tracer com filtros aplicados para protocolos **DHCP**, foi possível acompanhar visualmente as quatro etapas do protocolo:

```
[Cliente]  ------- DHCP Discover (Broadcast) -------> [Servidor]
[Cliente]  <------ DHCP Offer (Unicast/Broadcast) --- [Servidor]
[Cliente]  ------- DHCP Request (Broadcast) --------> [Servidor]
[Cliente]  <------ DHCP ACK (Unicast/Broadcast) ----- [Servidor]

```

1. **DHCP Discover:** O host inicializa sem IP e envia um pacote em broadcast procurando servidores DHCP disponíveis no domínio de broadcast.

2. **DHCP Offer:** O servidor responde oferecendo uma concessão com um endereço IP disponível no pool (`192.168.1.X`), máscara e gateway.

3. **DHCP Request:** O cliente formaliza o pedido aceitando o endereço oferecido.

4. **DHCP ACK (Acknowledgment):** O servidor confirma a alocação e grava a concessão.

## 🚀 Como Executar o Projeto

1. Baixe e instale o [Cisco Packet Tracer](https://www.netacad.com/courses/packet-tracer).

2. Clone este repositório:

   ```
   git clone https://github.com/SEU_USUARIO/lab-dhcp-packet-tracer.git
   
   ```

3. Abra o arquivo `topologia.pkt` diretamente no software.

4. Alterne para a aba **Simulation** e clique no botão de reprodução/passo a passo para ver o tráfego de pacotes na rede.

## 👤 Autor

Desenvolvido por **\[Seu Nome\]**

* [LinkedIn](https://www.linkedin.com/in/SEU_PERFIL/)

* [GitHub](https://github.com/SEU_USUARIO/)