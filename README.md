# 📡 Configuração de Roteamento com RIP - Passo a Passo

<img width="1874" height="697" alt="Captura de tela 2026-04-13 205904" src="https://github.com/user-attachments/assets/b8daa91d-fca1-40ba-82d6-6aebe3db0061" />


Este documento apresenta a configuração de um roteador Cisco no Packet Tracer utilizando roteamento dinâmico com RIP.

A explicação segue uma ordem lógica de execução, ideal para estudo e prática.

---

## 🧭 Etapa 1 — Acesso ao modo privilegiado

```bash
enable
```

**Explicação:**  
Entra no modo privilegiado do roteador (#), permitindo executar comandos administrativos e de configuração.

---

## 🧭 Etapa 2 — Entrar no modo de configuração global

```bash
configure terminal
```

**Explicação:**  
Permite alterar configurações do roteador.  
Todos os comandos principais de configuração são feitos aqui.

---

## 🧭 Etapa 3 — Definir nome do roteador

```bash
hostname SP
```

**Explicação:**  
Define o nome do roteador para identificação na rede.  
Boa prática para organização em ambientes com vários dispositivos.

---

## 🧭 Etapa 4 — Configurar interface LAN

```bash
interface f0/0
```

**Explicação:**  
Acessa a interface FastEthernet 0/0, normalmente conectada à rede local (LAN).

### 🔹 Definir endereço IP

```bash
ip address 192.168.45.1 255.255.255.0
```

**Explicação:**  
Define o IP da interface.  
Esse endereço será o gateway da rede local.

### 🔹 Ativar a interface

```bash
no shutdown
```

**Explicação:**  
Liga a interface.  
Por padrão, interfaces vêm desativadas.

### 🔹 Documentar a interface

```bash
description LAN SP
```

**Explicação:**  
Adiciona uma descrição para facilitar identificação futura.

---

## 🧭 Etapa 5 — Configurar interface WAN (Serial)

```bash
interface s0/0
```

**Explicação:**  
Acessa a interface serial, utilizada para comunicação entre roteadores (WAN).

### 🔹 Definir IP da WAN

```bash
ip address 30.0.0.1 255.0.0.0
```

**Explicação:**  
Define o endereço da rede entre roteadores.

### 🔹 Ativar a interface

```bash
no shutdown
```

**Explicação:**  
Ativa a interface serial.

### 🔹 Descrever o link

```bash
description LINK SP-RJ
```

**Explicação:**  
Identifica o link entre roteadores.

### 🔹 Definir largura de banda

```bash
bandwidth 512
```

**Explicação:**  
Define a largura de banda lógica (Kbps).  
Utilizado por protocolos de roteamento para cálculo de métricas.

### 🔹 Configurar clock (somente DCE)

```bash
clock rate 500000
```

**Explicação:**  
Define a taxa de clock da interface serial.  
Só deve ser configurado no lado DCE da conexão.

---

## 🧭 Etapa 6 — Configurar protocolo RIP

```bash
router rip
```

**Explicação:**  
Ativa o protocolo de roteamento dinâmico RIP.

### 🔹 Informar rede WAN

```bash
network 30.0.0.0
```

**Explicação:**  
Define que a rede WAN será anunciada para outros roteadores.

### 🔹 Informar rede LAN

```bash
network 192.168.45.0
```

**Explicação:**  
Permite que outras redes conheçam a LAN local.

---

## 🧭 Etapa 7 — Sair da configuração

```bash
end
```

**Explicação:**  
Sai do modo de configuração e volta ao modo privilegiado.

---

## 🧭 Etapa 8 — Salvar configuração

```bash
copy running-config startup-config
```

**Explicação:**  
Salva a configuração atual na memória permanente.  
Evita perda de dados ao reiniciar o roteador.

---

## 🔄 Resumo do funcionamento

- O roteador conecta uma rede local (LAN) a outras redes  
- As conexões entre roteadores são feitas via WAN (serial)  
- O protocolo RIP permite que as rotas sejam aprendidas automaticamente  
- Cada roteador anuncia suas redes para os demais  

---

## 🧪 Teste de funcionamento

Após configurar todos os roteadores:

```bash
ping 192.168.X.X
```

**Resultado esperado:**  
Comunicação entre diferentes redes funcionando corretamente.

---

## 📌 Observações importantes

- Interfaces devem estar sempre com `no shutdown`  
- `clock rate` só no lado DCE  
- RIP utiliza métrica baseada em número de saltos (hop count)  
- Redes devem ser corretamente declaradas no RIP  

