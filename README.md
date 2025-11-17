# Brute-force-com-Medusa-

### 3.1 FTP (Metasploitable 2)

**Objetivo.** Verificar se havia **senhas fracas** no serviço **FTP (vsftpd 2.3.4)** do ambiente de laboratório.

**Insumos.** Listas **curtas**:
- `users.txt`: `user`, `msfadmin`, `admin`, `root` (4 usuários)
- `pass.txt`: `123456`, `password`, `qwerty`, `msfadmin` (4 senhas)

**Configuração responsável.** Tentativas **limitadas**, com concorrência moderada, e **interrupção após confirmar o primeiro sucesso** (sem pós-exploração).

**Resultados (resumo).**
- **Alcance e serviços** confirmados no alvo do lab (ICMP OK; `21/tcp ftp` aberto).  
- **Total de combinações testadas:** 16 (4×4).  
- **Sucesso encontrado:** `m***n` + `m******n` (mascarado).  
- **Comportamento do serviço:** mensagens de erro genéricas; sem bloqueio progressivo aparente.

**Tabela-resumo.**

| # | Usuário (masc.) | Senhas testadas | Status    | Observações                         |
|--:|------------------|-----------------|-----------|-------------------------------------|
| 1 | u***r            | 4               | Falha     | Sem bloqueio aparente               |
| 2 | m***n            | 4               | **Sucesso** | Senha comum (mascarada); teste encerrado |
| 3 | a***in           | 4               | Falha     | —                                   |
| 4 | r**t             | 4               | Falha     | —                                   |

**Evidências.**
  <img width="663" height="507" alt="b5854fae-d442-48c1-af30-a135aa99efd8" src="https://github.com/user-attachments/assets/cf6ae6fb-02b7-4e08-b3c1-c1356a51c41a" />

*Figura 1 — Ping/Nmap: alvo ativo e FTP aberto no lab (rede host-only).*

  <img width="763" height="294" alt="efeb18d1-563e-44f4-8eed-bbd6ab034534" src="https://github.com/user-attachments/assets/92649d4a-3f47-45d4-871a-65a7a910f730" />

*Figura 2 — Tentativa manual com credenciais fracas → falha.*

<img width="744" height="499" alt="88617f34-cd80-4407-8981-65443efa06de" src="https://github.com/user-attachments/assets/e3dce098-9d97-407b-bba1-5e44752ed1e1" />

*Figura 3 — Criação de `users.txt` / `pass.txt` e checagem de parâmetros do auditor de login.*

<img width="783" height="509" alt="521cb040-5b24-466f-b45b-869363e19407" src="https://github.com/user-attachments/assets/dff8f1bd-39b9-4e20-80fb-81b2867edcc3" />

*Figura 4 — Auditoria de login: combinações limitadas; registro das tentativas.*
  
*Figura 5 — **[SUCCESS]** com dados **mascarados**.*
<img width="777" height="34" alt="0f2d257b-3854-4423-ad74-801b61b17b0e" src="https://github.com/user-attachments/assets/c6f265c8-3ee0-4d18-8b0a-a096ce7967cd" />

  
*Figura 6 — Confirmação mínima de login após o sucesso; sem pós-exploração.*
<img width="405" height="303" alt="15592e78-1c15-4b66-889d-2aba658313e0" src="https://github.com/user-attachments/assets/7d9e63b8-2a4e-4135-b2af-6add6e2abc50" />

**Mitigações (recomendadas).**
- **Política de senhas** (comprimento/complexidade/histórico) e **bloquear senhas comuns**.  
- **MFA** quando aplicável.  
- **Bloqueio progressivo**/atraso entre tentativas; **mensagens de erro genéricas**.  
- Preferir **SFTP/FTPS**; desabilitar **FTP** puro quando possível.  
- **Monitoramento & logs** com alertas de tentativas repetidas.

> **Nota ética:** Teste realizado **somente** em laboratório (VMs, rede host-only), com **tentativas limitadas** e **sem pós-exploração**.
