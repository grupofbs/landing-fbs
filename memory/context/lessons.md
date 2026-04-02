# Lições Aprendidas

> Erros e padrões que não podem se repetir.
> 🔒 Estratégicas = permanentes | ⏳ Táticas = expiram em 30 dias

## 🔒 Estratégicas (Permanentes)

### Config OpenClaw — chaves corretas (02/04/2026)
- `dmAllowlist` NÃO existe → chave correta é `allowFrom` com formato `"tg:ID"`
- Serviço systemd é user-level: `systemctl --user restart openclaw-gateway`
- Depois de restart, pode precisar re-parear devices: `openclaw devices list` → `openclaw devices approve --latest`

### Memória é arquivo, não mente (02/04/2026)
- "Mental notes" morrem na próxima sessão
- Se importa → escreve em arquivo
- Se Nilton disse → registra imediatamente
- NUNCA confiar na memória de sessão pra algo que precisa persistir

### Nilton odeia repetir (02/04/2026)
- Se ele já explicou algo, está em memory/
- Antes de perguntar, buscar com memory_search
- Se não achar, aí sim perguntar

## ⏳ Táticas (Revisar em 30 dias)

### Gateway pairing após restart (02/04/2026)
- CLI local perde pairing após restart do gateway
- Solução: `openclaw devices approve --latest`
- Cron tool funciona via sessão ativa mesmo quando CLI está sem pairing

---

*Atualizado: 2026-04-02*
