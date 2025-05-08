# 🛠️ Projeto Cisco Packet Tracer: Diagnóstico de Conectividade com Ping, Traceroute e Netstat

## 🎯 Objetivo

Demonstrar a interligação de duas sub-redes diferentes usando apenas **uma interface física no roteador**, por meio de **subinterfaces com VLANs** e um **switch em modo trunk**.

---

## 📦 Equipamentos utilizados

- 1 Roteador Cisco (ex: 1841 ou 2911)
- 1 Switch Cisco gerenciável (ex: 2960)
- 2 PCs
- Cabos diretos (cobre)

---

## 🧱 Plano de Endereçamento e VLANs

| Sub-rede         | IP do PC        | Gateway no Roteador | VLAN |
|------------------|-----------------|----------------------|------|
| 192.168.10.0/24  | 192.168.10.10   | 192.168.10.1         | 10   |
| 192.168.20.0/24  | 192.168.20.10   | 192.168.20.1         | 20   |

---

## 🔌 Conexões

- PC Desenvolvimento → Switch Fa0/1  
- PC Infraestrutura → Switch Fa0/2  
- Switch Fa0/24 → Roteador Fa0/0  

---

## 🔧 Etapas principais de configuração

### 🖧 Roteador: Subinterfaces com 802.1Q

```bash
enable
configure terminal

interface FastEthernet0/0.10
encapsulation dot1Q 10
ip address 192.168.10.1 255.255.255.0

interface FastEthernet0/0.20
encapsulation dot1Q 20
ip address 192.168.20.1 255.255.255.0

interface FastEthernet0/0
no shutdown
enable
configure terminal

vlan 10
name Desenvolvimento

vlan 20
name Infraestrutura

interface fastEthernet 0/1
switchport mode access
switchport access vlan 10

interface fastEthernet 0/2
switchport mode access
switchport access vlan 20

interface fastEthernet 0/24
switchport mode trunk

```

## ✅ Testes de Conectividade

Acesse o **Command Prompt** de cada PC (aba "Desktop") e execute os testes:

---

### 🔁 1. Ping

```bash
ping 192.168.20.10   # Do PC Desenvolvimento para PC Infraestrutura
ping 192.168.10.10   # Do PC Infraestrutura para PC Desenvolvimento
```
Se tudo estiver correto, o ping será bem-sucedido.

---

### 🛰️ 2. Traceroute (Tracert)
```bash
tracert 192.168.20.10   # A partir do PC Desenvolvimento
```
Mostra o caminho dos pacotes até o destino, incluindo o roteador.

---

### 📡 3. Netstat
```bash
netstat
```
Mostra conexões ativas (se houver), como simulações de serviços ou respostas de ping.


## 🖼️ Capturas de Tela

### 🔌 Topologia da Rede
> Estrutura completa com os 2 PCs, switch e roteador conectados.
![Topologia da Rede]()

---

### 💻 PC Desenvolvimento – Configuração de Rede
> Mostra o modelo, IP, MAC Address e Gateway configurado no PC1.
![PC1 Detalhes]()

---

### 💻 PC Infraestrutura – Configuração de Rede
> Mostra o modelo, IP, MAC Address e Gateway configurado no PC2.
![PC2 Detalhes]()

---

### 📶 Switch Detalhes
> Apresenta o modelo do switch (2960) e as portas que estão conectadas aos dispositivos.
![Switch Detalhes]()

---

### 🌐 Roteador Detalhes
> Informações do roteador (1841), portas conectadas e IP configurado na interface.
![Roteador Detalhes]()


## 📂 Arquivos Incluídos

- `Diagnóstico de Conectividade com Ping`: Arquivo da simulação no Cisco Packet Tracer
- `README.md`: Este documento explicando o projeto

## 👩‍💻 Autora

Biatriz Gomes

---
