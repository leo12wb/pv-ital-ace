# Findings — linux-030.html

## Estrutura geral
- ~1735 linhas totais
- CSS inline no `<head>` (~575 linhas)
- HTML body (~160 linhas)
- JS inline no `<script>` (~1000 linhas)

## Arrays de dados
| Array | Papel |
|-------|-------|
| `disciplinas[]` | Alimenta Resumo (acordeão) e Flashcards automáticos |
| `questoes[]` | Banco do Quiz rápido |
| `EXAMES_DATA[]` | Simulados completos com seções |

### Formato `disciplinas`
```js
{ nome: "🎨 Label", cor: "linear-gradient(...)", topicos: [
  { t: "Termo", d: "Descrição longa", freq: "alto|medio|baixo" }
]}
```

### Formato `questoes`
```js
{ disc: "Label curto", p: "Pergunta?", ops: ["A","B","C","D"], c: 1, exp: "Explicação." }
// c = índice da opção correta (0-based)
```

### Formato `EXAMES_DATA`
```js
{ id: 'sim1', titulo: '...', banca: '...', ano: 2025, edital: '...', cargo: '...',
  secoes: [{ nome: 'Seção (Q1–Q10)', qs: [
    { n:1, q:'Pergunta', ops:['A','B','C','D'], g:0, exp:'...' }
    // g = índice do gabarito (0-based)
  ]}]
}
```

## Funções JS críticas (todas devem ser copiadas)
- `buildFlashDados()` — deriva flashcards dos tópicos
- `renderResumo()` — acordeão
- `renderMapa()` — grid de cards
- `renderCard()` — flashcard atual
- `iniciarQuiz()` / `renderQuestao()` / `verificarResposta()`
- `renderExamesList()` / `iniciarExame()` / `responderExame()` / `finalizarExame()`
- `mostrarRelatorioHorario()` / `exportarTXT()`
- `falar()` / `falarCard()` — TTS
- `toggleDark()` / `mudarTab()` / `toast()`

## Variáveis globais necessárias
- `flashDados`, `flashDeck`, `flashIdx`
- `quizPerguntas`, `quizIdx`, `quizCertas`, `quizErradas`, `respondeu`
- `exAtual`, `exSecAtual`, `exQAtual`, `exRespostas`, `exStarted`
- `_speechRate`
- `STORAGE_KEY` → mudar para `'aceRespostas'`

## Paleta original (blue) → nova (green)
| Variável | Original | Nova |
|----------|----------|------|
| `--lpi-primary` | `#0369a1` | `#15803d` |
| `--lpi-secondary` | `#0284c7` | `#16a34a` |
| `--ciano` | `#0891b2` | `#0d9488` |
| `--azul` | `#0ea5e9` | `#22c55e` |
| Header gradient | `#022040→#0369a1→#0284c7` | `#052e16→#15803d→#16a34a` |
| dark hover bg | `#082244` | `#052e16` |
| dark quiz badge bg | `#0c2a44` | `#052e16` |
