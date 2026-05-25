# Simulador da Copa do Mundo 2026

## Stack
- HTML/CSS/JS puro, single-file (index.html)
- Sem build step, sem framework, sem dependências externas além de Google Fonts
- Hospedado na Vercel via integração com GitHub

## Estrutura do código
Todo o código está em index.html, dividido em:
- <style>: design system com tokens CSS em :root
- <script>: dados (TEAMS, SCHEDULE, GOAL_PROBS, PK_PROBS), simulação,
  fase de grupos, mata-mata e renderização

## Convenções
- Fontes: Bebas Neue (títulos), Anton (placares), Manrope (corpo),
  JetBrains Mono (metadata)
- Cores semânticas: --accent (verde, gramado), --accent-2 (dourado),
  --accent-3 (rosa, atenção), --accent-4 (azul)
- Toda mudança visual deve respeitar os tokens CSS — não usar cores hardcoded

## Modelo estocástico
- Probabilidade de vitória/empate/derrota baseada em pontos FIFA + ranking
- 15% das partidas têm resultado aleatório (RANDOM_RATE)
- Gols vêm da distribuição empírica das Copas 2010-2022 (GOAL_PROBS)
- Pênaltis usam taxas históricas por ordem de cobrança (PK_PROBS)
- Mata-mata: empate → prorrogação (Poisson) → pênaltis se persistir

## Regras FIFA implementadas
- Desempate no grupo: confronto direto → SG geral → GP → Ranking FIFA
- 8 melhores 3º colocados via backtracking nas 495 combinações possíveis
- Chaveamento M73–M104 conforme regulamento oficial

## Coisas a evitar
- Não remova as constantes RANDOM_RATE, GOAL_PROBS, PK_PROBS sem justificar
- Não troque o layout do bracket sem revalidar as conexões M89→M104
