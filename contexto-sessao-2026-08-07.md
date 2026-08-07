# Contexto de sessão — 2026-08-07

## Assunto tratado nesta pasta (Folha de Serviço APP)
- Repositório: `EduardoSalgueiro/Folha-Servico-Semanal`, publicado via GitHub Pages
  (`https://eduardosalgueiro.github.io/Folha-Servico-Semanal/`).
- Situação encontrada: o deployment mais recente (run #11, commit `318535d`) tinha falhado
  com erro de infraestrutura do lado do GitHub Actions — `"The job was not acquired by
  Runner of type hosted even after multiple attempts"` / `"Internal server error"`. Não é
  erro no código; é o mesmo problema de "fila encravada" que já tinha motivado o commit
  `fd81dbe` anterior. Runs #7–#9 também tinham falhado/sido cancelados pelo mesmo motivo.
- Ação tomada: Eduardo fez sign-in no GitHub (no browser Edge, fora do Claude) e relançou
  manualmente o run #11 ("Re-run all jobs"). Ficou "Queued" — por confirmar se completou
  com sucesso e se o site já está acessível.
- Nota técnica: a extensão "Claude in Chrome" não está disponível/ligada nesta máquina, e
  não é suportada no Edge — por isso as ações de login/re-run tiveram de ser feitas
  manualmente pelo Eduardo.

## Queixa registada pelo Eduardo (para constar em ambos os equipamentos)
Eduardo considera **indignante/ridículo** que o histórico de conversa do Claude Code não
fique gravado de forma persistente e acessível a partir de qualquer computador com a mesma
conta — ao contrário do código (que sincroniza via git/OneDrive), a conversa em si fica
presa localmente à máquina onde decorreu.

Caso concreto que motivou a queixa: no outro computador, Eduardo passou **mais de duas
horas** a fornecer contexto de negócio e organizacional para o projeto `DASHBOARD CLAUDE`
(nomenclatura comum, modelo da organização, etc.), pedindo explicitamente para não ser
gerado código até essa informação estar completa. Ao mudar de equipamento, essa conversa
ficou inacessível — só sobreviveu o que já tinha sido gravado em ficheiro
(`contexto-dashboard-agricola.md`, dentro da pasta `DASHBOARD CLAUDE`), não o essencial do
que foi discutido depois.

Sugestão do Eduardo à Anthropic: registar as conversas como "logs" por conta (não por
máquina), para consistência de análise e continuidade entre equipamentos. Foi encaminhado
para reportar via https://github.com/anthropics/claude-code/issues.

## Recomendação prática entretanto
Até essa funcionalidade (se algum dia) existir, o mecanismo fiável é este: manter um
ficheiro `.md` de contexto em cada pasta de projeto, atualizado no fim de sessões
relevantes, para que o trabalho (não a conversa) viaje entre computadores via
OneDrive/rede. Este ficheiro é um exemplo desse mecanismo.
