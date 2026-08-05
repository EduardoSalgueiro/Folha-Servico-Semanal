# Contexto do Projeto — Folha de Serviço Semanal (Monte de Sampaio)

## Objetivo geral
Eduardo (gestor na empresa agrícola "Monte de Sampaio") está a usar IA para melhorar métodos
de trabalho: reduzir procrastinação, depender menos de interrupções constantes de terceiros,
e ter dados/ferramentas próprias em vez do software de gestão agrícola da empresa (considerado
mau e pouco intuitivo). Abordagem: prova de conceito primeiro com dados reais, validar, só
depois evoluir para metodologia de trabalho efetiva.

## Ficheiro atual
`folha-servico-semanal.html` — app mobile-first que substitui a folha de papel semanal
(baseada num PDF original dos colaboradores).

Campos e regras:
- **Nome**: lista fechada (Figueira, Serrado, Pedro Figueira, Rui Ribeiro, Cornel), bloqueada
  após o 1º registo do dia; botão "Trocar colaborador" avisa e limpa a lista
- **Semana**: input `date` + cálculo automático da semana ISO + intervalo Seg–Dom visível
  (substitui `input type="week"`, que falhava no Safari iOS)
- **Data/Horas/Extras**: limpos após cada "Adicionar", sem valores por defeito
- **Serviço**: dropdown "Com folha" (Poda, Topping, Baixeiras, Trat. Foliar, Erva, Rama,
  Herbicida, Adubo/Mat. Org., Raticida, Burricos, Colheita, Colheita Carrego) e "Sem folha"
  (Cons.Rep.Parcelas/Caminhos, Cons.Rep.Equip/Máquinas, Rega e Manutenção, Vacas,
  Outros(Agricultura), Monte/Casa Moura, Casas) — sem pré-seleção, obriga escolha ativa
- **Local**: lista fechada (Manantiz, Bico, Ent.Drtª, Ent.Esqdª, 24 Horas, Frente Monte,
  Trás do Monte, Poço, Várzea, Vacas, Charnequinha, Charnequinha Nova Plantação)
- **Obs**: opcional
- Resumo diário com badges "✓ 8h completas" / "⚠ faltam Xh" — **extras não contam para as 8h**
- Confirmação não-bloqueante (`confirm()`) ao Guardar/Enviar se o dia estiver incompleto
- Exportação Excel (SheetJS): sem linhas de identificação no topo, nome da aba = nome do
  colaborador, filtros de cabeçalho em todas as colunas (incluindo Semana, para consolidação
  futura — Eduardo vai juntar as folhas de todos os colaboradores num único Excel, uma
  aba por colaborador, e montar tabelas dinâmicas por Atividade/Operação/Colaborador)
- Exportação guarda sempre cópia local no telemóvel primeiro, depois tenta Web Share API
  (para WhatsApp)
- Ícone/favicon/apple-touch-icon com o logótipo embutido
- Título: "Monte de Sampaio — Folha de Serviço"
- Distribuição planeada: link direto por WhatsApp, com ícone no ecrã principal do telemóvel
- **Estado: completo e funcional dentro do Claude**

## Limitação crítica descoberta (por resolver)
`window.storage` (guardar automático/rascunho) só funciona com sessão Claude iniciada —
confirmado por teste real num iPhone via link publicado (pediu login ao selecionar
colaborador). Isto inviabiliza depender de storage para colaboradores sem conta Claude.

**Solução já pensada mas ainda não implementada**: remover a dependência de
`window.storage`; usar o próprio Excel exportado como "ponto de restauro" — adicionar um
botão "Importar rascunho" (usando o SheetJS já carregado) que lê um Excel já exportado
anteriormente e repõe os serviços na lista, permitindo continuar sem login. Fluxo: exportar
serve tanto de checkpoint como de envio final; importar repõe o rascunho.

## Motivo da migração para Claude Code
Ao publicar a página no Claude, o ícone mostrado é o do Claude, não o logótipo da empresa —
mesmo com favicon/apple-touch-icon customizados no HTML (ainda por confirmar se resolve).
Alojar como app própria fora do Claude (ex.: GitHub Pages/Netlify) resolveria isto e também
o problema do login/storage. Eduardo já confirmou ter o plano Pro (necessário para Claude
Code) e está a instalar o Git for Windows como pré-requisito.

## Ficheiros de origem usados no desenvolvimento
PDF da folha de serviço original em papel, e o logótipo da empresa (já embutido em base64
no HTML).

## Outras pendências
- Validação de sobreposição de horas num mesmo dia foi mencionada como requisito inicial
  mas nunca implementada (ficou substituída pela validação simples das 8h/dia) — pode
  ainda ser pedida
- Consolidação final num único Excel (múltiplas abas, uma por colaborador) é, por agora,
  processo manual do próprio Eduardo

