# Jogo da Velha — Máquina do Tempo

![Banner colorido do Jogo da Velha — Máquina do Tempo](assets/banner-jogo-da-velha.svg)

Um jogo da velha **100% offline**, desenvolvido para transformar um exercício clássico em uma experiência de estratégia com identidade visual própria. Além de disputar partidas entre X e O, a pessoa usuária pode voltar no tempo ao fim de cada rodada e rever cada decisão, lance a lance.

## Objetivos do projeto

- Aplicar HTML5 semântico, CSS3 responsivo e JavaScript ES2020 sem bibliotecas externas.
- Demonstrar uma arquitetura MVC clara, separando regras do jogo, renderização e eventos.
- Oferecer uma interface inclusiva, navegável por teclado e informativa para leitores de tela.
- Criar um diferencial didático: a **Máquina do Tempo**, um replay da partida concluída.

## Demonstração e execução local

Não há instalação, build ou conexão com a internet. Basta abrir `index.html` em um navegador moderno.

Como alternativa, é possível iniciar um servidor local na pasta do repositório:

```bash
python3 -m http.server 8000
```

Depois, acesse [http://localhost:8000](http://localhost:8000) no navegador.

## Funcionalidades (RF)

| ID | Requisito funcional | Implementação |
| --- | --- | --- |
| RF01 | Exibir um tabuleiro 3 × 3 interativo. | Nove botões nativos formam a grade do jogo. |
| RF02 | Alternar os jogadores automaticamente. | X começa todas as partidas e a vez muda após um lance válido. |
| RF03 | Impedir lances inválidos. | Casas ocupadas, bem como um tabuleiro encerrado, não aceitam jogadas. |
| RF04 | Reconhecer vitória e empate. | O modelo avalia as oito linhas vencedoras e o preenchimento total da grade. |
| RF05 | Manter o placar entre partidas. | Vitórias de X, vitórias de O e empates são atualizados ao final da rodada. |
| RF06 | Criar uma nova partida. | Limpa somente a grade e o histórico da rodada atual, preservando o placar. |
| RF07 | Zerar o placar com confirmação. | Um diálogo modal exige confirmação explícita antes de apagar a pontuação. |
| RF08 | Reproduzir uma partida concluída. | Os controles **Jogada anterior** e **Próxima jogada** percorrem o histórico sequencial. |

## Requisitos não funcionais (RNF)

| ID | Requisito não funcional | Atendimento |
| --- | --- | --- |
| RNF01 | Execução offline. | Todos os arquivos são locais; não há dependências, fontes remotas ou APIs. |
| RNF02 | Responsividade. | CSS Grid e Flexbox, unidades fluidas e regra mobile garantem adaptação sem rolagem horizontal. |
| RNF03 | Acessibilidade WCAG AA. | Botões nativos, foco visível, contraste elevado, rótulos ARIA dinâmicos e região de status ao vivo. |
| RNF04 | Compatibilidade. | JavaScript puro ES2020 e elementos HTML5 suportados por navegadores modernos. |
| RNF05 | Manutenibilidade. | Classes Model, View e Controller mantêm responsabilidades isoladas e código comentado. |
| RNF06 | Preferências de movimento. | Animações são reduzidas quando `prefers-reduced-motion` está ativo. |

## Regras de negócio

1. O jogador **X** inicia toda nova partida.
2. Uma casa só pode receber uma marca uma vez; clicar nela novamente não altera o turno.
3. Após cada lance válido, o jogo verifica as **8 combinações vencedoras**: três linhas, três colunas e duas diagonais.
4. A rodada termina imediatamente quando há uma trinca ou quando as nove casas são preenchidas sem vencedor.
5. Ao encerrar a rodada, o tabuleiro é bloqueado e o resultado atualiza uma única vez o placar correspondente.
6. A opção **Nova partida** reinicia a rodada com X, mas não apaga as estatísticas.
7. A opção **Zerar placar** não afeta a rodada em andamento; ela apenas redefine vitórias e empates após confirmação.
8. A Máquina do Tempo só aparece ao fim da rodada e é somente leitura: ela reconstrói o tabuleiro a partir do histórico, sem modificar o resultado ou o placar.

## Arquitetura MVC

O código JavaScript segue uma divisão intencional de responsabilidades:

```text
Evento de interface → GameController → GameModel → GameView
        ▲                                   │
        └──────── renderização do estado ───┘
```

- **`GameModel`**: contém o tabuleiro, jogador atual, histórico, placar e todas as regras de vitória, empate e replay. Não acessa o DOM.
- **`GameView`**: consulta os elementos da página e atualiza conteúdo, classes CSS, estados bloqueados e atributos de acessibilidade. Não contém regras de negócio.
- **`GameController`**: escuta os eventos dos botões, coordena chamadas entre Model e View e controla a posição do replay.

## Acessibilidade e interação

- Use <kbd>Tab</kbd> para navegar entre os controles e <kbd>Enter</kbd> ou <kbd>Espaço</kbd> para ativar o botão em foco.
- Cada célula informa linha, coluna e ocupação em seu `aria-label`, que é atualizado após uma jogada.
- O painel de status utiliza `role="status"` e `aria-live="polite"` para anunciar mudanças de turno e resultados.
- A identidade dos jogadores não depende apenas de cor: as marcas **X** e **O**, os textos e os rótulos acessíveis comunicam o estado.

## Estrutura do repositório

```text
.
├── assets/
│   └── banner-jogo-da-velha.svg  # Banner vetorial do projeto
├── app.js                        # Model, View e Controller
├── index.html                    # Estrutura e semântica da interface
├── styles.css                    # Tema, responsividade e estados visuais
└── README.md                     # Documentação do projeto
```

## Tecnologias

- HTML5
- CSS3 (Grid, Flexbox, media queries e variáveis)
- JavaScript ES2020

## Autoria

Projeto educacional de front-end criado como uma implementação autônoma de Jogo da Velha com replay interativo.
