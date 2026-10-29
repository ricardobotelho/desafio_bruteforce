<h2 align="center">
    Santander 2026 - Cibersegurança do Zero a prática
<br><br>
📚 Ataque de Brute Force com Medusa e Kali Linux
<h2>

<p align="center">
    <a href="#-objetivo">Objetivo</a>&nbsp;&nbsp;|&nbsp;&nbsp;
    <a href="#-reflexões">Reflexões</a>&nbsp;&nbsp;|&nbsp;&nbsp;
    <a href="#-protocolos">Protocolos</a>&nbsp;&nbsp;|&nbsp;&nbsp;
    <a href="#-síntese-defensiva">Síntese Defensiva</a>&nbsp;&nbsp;|&nbsp;&nbsp;
    <a href="#-conclusão">Conclusão</a>&nbsp;&nbsp;|&nbsp;&nbsp;
</p>
<br>


<br><br>
## 🎯 Objetivo

É registrar os passos executados, mas consolidar a compreensão sobre como funcionam os ataques de força bruta, por que sistemas continuam vulneráveis e como aplicar defesas eficazes no ciclo de desenvolvimento e administração de sistemas.


<br><br>
## 💡 Reflexões

### 1. A Importância da Higiene de Credenciais
Durante a simulação no ambiente controlado, ficou evidente que a maior parte dos acessos não autorizados ocorre devido ao uso de credenciais padrão (*default credentials*) ou senhas fracas presentes em dicionários comuns. 
* **Reflexão:** Ferramentas automatizadas como o **Medusa** não realizam "mágica", elas apenas exploram a previsibilidade humana na escolha de senhas. A conscientização de usuários e administradores é tão crítica quanto a implementação de barreiras técnicas.

### 2. Diferença Entre Ataques Paralelos e Sequenciais
Ajustar o número de threads e a agressividade do ataque altera drasticamente o comportamento e a visibilidade nos logs do sistema alvo.
* **Reflexão:** Ataques muito rápidos podem gerar negação de serviço (DoS) involuntária ou disparar alarmes em sistemas de detecção de intrusão (IDS). Entender a taxa de requisições por segundo permitida pelo protocolo (ex: HTTP vs. SMB) é fundamental para auditorias e dimensionamento de controles defensivos.

### 3. Password Spraying vs. Brute Force Tradicional
No teste realizado via SMB, a abordagem de *Password Spraying* (testar uma única senha comum contra uma lista de múltiplos usuários) demonstrou a importância de estratégias que evitam o bloqueio de contas (*Account Lockout*).
* **Reflexão:** Controles defensivos baseados apenas na contagem de erros consecutivos por usuário podem ser facilmente contornados por um atacante que distribui as tentativas ao longo do tempo ou entre múltiplos nomes de usuário.


<br><br>
## 🔬 Protocolos

### A. Protocolo FTP (Porta 21)
* **Comportamento:** Comunicação em texto claro.
* **Vulnerabilidade Conceitual:** O envio do par usuário/senha em texto puro permite interceptação (Sniffing) na rede local, além de ser um alvo clássico para ataques de dicionário por não possuir limite nativo de tentativas no protocolo básico.

### B. Formulários Web e Controle de Sessão (HTTP)
* **Comportamento:** O envio de credenciais ocorre via requisições POST ou GET.
* **Vulnerabilidade Conceitual:** Formulários sem verificação de Captcha, limitação de taxa (Rate Limiting) ou Tokens Anti-CSRF abrem margem para automação de requisições HTTP em alta velocidade.

### C. Serviço SMB / Samba (Porta 139/445)
* **Comportamento:** Autenticação baseada em desafios e respostas (NTLM/Kerberos).
* **Vulnerabilidade Conceitual:** Permite a enumeração de nomes de usuários válidos via chamadas RPC/NetBIOS, facilitando a criação de dicionários direcionados.


<br><br>
## 🛡️ Síntese Defensiva

A partir dos cenários estudados, foram consolidados os seguintes pilares de proteção:

1. **Defesa em Profundidade (Defense-in-Depth):**
   * Não confiar em apenas um controle. Combinar senhas fortes, MFA e monitoramento de logs.
2. **Implementação de Rate Limiting e Lockout:**
   * Configurar ferramentas como `Fail2ban` no ecossistema Linux e políticas de bloqueio de conta no Active Directory.
3. **Monitoramento e Alertas:**
   * Configurar SIEM para alertar sob picos atípicos de respostas HTTP `401 Unauthorized` ou falhas de autenticação no syslog.


<br><br>
## 🏁 Conclusão

A realização deste desafio permitiu consolidar a visão prática dos riscos associados à gestão inadequada de identidades e acessos. A experiência prática com o **Medusa** e as ferramentas de suporte reforçou a importância de atuar com uma postura proativa na identificação e correção de fragilidades antes que possam ser exploradas de forma maliciosa.


<br><br>
## 🤝 Contribuidores

<a href="https://github.com/ricardobotelho"><img src="https://github.com/ricardobotelho.png" width="45" height="45"></a> &nbsp;