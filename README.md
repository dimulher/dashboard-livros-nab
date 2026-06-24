# Dashboard — Correção de Livros NAB

Dashboard em tempo real para acompanhar o progresso da correção de capítulos dos livros NAB.

**Visualize em produção:** https://dashboard-livros-nab.vercel.app

---

## Como funciona?

1. **Dados em `dados.json`** — estrutura hierárquica (Dede vs Robert → Livros → Coordenadores → Autores)
2. **HTML lê `dados.json`** e renderiza lado a lado
3. **Sincronização automática** — a cada 30 segundos, recarrega os dados
4. **Deploy em Vercel** — qualquer `git push` atualiza o site automaticamente

---

## Atualizando o Dashboard

### Quando fazer uma correção:

1. Corrija o capítulo (Fase 1 — veja `INSTRUCOES-SISTEMA-CORRECAO.md`)
2. Abra `dados.json`
3. Encontre seu nome (Dede ou Robert) → seu livro → coordenador → autor
4. Atualize:
   ```json
   {
     "nome": "Julio Serotini",
     "status": "concluido",     // mude de "pendente" para "concluido"
     "data": "2026-06-24",      // data de hoje
     "creditos": 2.59           // creditos que GPT-5.5 consumiu
   }
   ```

5. Faça `git commit` e `git push`
6. Dashboard atualiza automaticamente em ~1 minuto

---

## Estrutura de `dados.json`

```json
{
  "ultima_atualizacao": "ISO-8601 timestamp",
  "dede": {
    "nome": "Dede",
    "cor": "#3B82F6",
    "livros": [
      {
        "nome": "HEROIS VOL 9",
        "coordenadores": [
          {
            "nome": "COORD-IRENE DE SA",
            "autores": [
              {
                "nome": "Julio Serotini",
                "status": "concluido|pendente|erro",
                "data": "2026-06-24",
                "creditos": 16.0
              }
            ]
          }
        ]
      }
    ]
  },
  "robert": {
    "nome": "Robert",
    "cor": "#EF4444",
    "livros": [...]
  }
}
```

---

## Status possíveis

- **`concluido`** 🟢 — capítulo corrigido e salvo
- **`pendente`** 🟡 — aguardando correção
- **`erro`** 🔴 — erro na correção (revisar)

---

## Deploy em Vercel

Este repositório está conectado ao Vercel.

**Fluxo automático:**
```
git push → GitHub → Vercel detecta mudança → rebuild → deploy
```

Você não precisa fazer nada — apenas `git push` com os dados atualizados!

---

## Checklist ao corrigir um capítulo

- [ ] Capítulo corrigido (Fase 1 completa)
- [ ] `dados.json` atualizado
- [ ] Status = "concluido"
- [ ] Data preenchida
- [ ] Créditos GPT-5.5 anotados
- [ ] `git add dados.json`
- [ ] `git commit -m "Update: [seu nome] corrigiu [Autor Nome]"`
- [ ] `git push`
- [ ] Verificar no dashboard em ~1 min

---

## Troubleshooting

**Dashboard não atualiza:**
- Aguarde 30 segundos (próximo refresh automático)
- Limpe cache do navegador (Ctrl+Shift+Del)
- Verifique se JSON está válido: https://jsonlint.com/

**Deploy não funciona:**
- Confirme que `dados.json` é JSON válido
- Verifique no GitHub se o push foi bem-sucedido
- Veja logs no Vercel: https://vercel.com/dashboard

---

Mantido por: dimulher  
Último update: 2026-06-24
