# carrossel-assessoria

Skill do Claude Code que gera carrosséis de Instagram (1080x1350 PNG) para os criadores da assessoria, em 5 estilos: Twitter, Clássico, Giz, Case e Documentação.

Antes de produzir, consulta a pasta do criador no Drive da assessoria (pasta Membros): lê onboarding, plano de ação e levas já entregues, monta a ficha do criador e sugere de 5 a 8 temas de carrossel com a fonte de cada um.

## Instalar

```bash
git clone https://github.com/claudiomarquespincho-netizen/carrossel-assessoria.git ~/carrossel-assessoria
ln -s ~/carrossel-assessoria ~/.claude/skills/carrossel-assessoria
```

Precisa do conector do Google Drive ligado na sessão e, para os prints do Instagram, do Claude in Chrome.

## Usar

- "sugere temas de carrossel pra Aninha"
- "carrossel pro João" (sem tema, ela sugere)
- "carrossel twitter pro Dr. Rafael: 5 mitos sobre testosterona" + áudio
