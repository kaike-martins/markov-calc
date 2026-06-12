# Calculadora de Cadeias de Markov

Ferramenta web para analisar cadeias de Markov em tempo discreto: você monta a matriz de transição, define onde o sistema começa e descobre a distribuição depois de quantas gerações quiser, além da distribuição de equilíbrio e da análise de absorção.

![JavaScript](https://img.shields.io/badge/JavaScript-vanilla-f7df1e)
![Sem dependências](https://img.shields.io/badge/depend%C3%AAncias-nenhuma-brightgreen)
![GitHub Pages](https://img.shields.io/badge/deploy-GitHub%20Pages-181717)

**Acesse:** https://kaike-martins.github.io/markov-calc/

<!-- Depois de subir um print da tela em docs/screenshot.png, descomente a linha abaixo:
![Captura de tela da calculadora](docs/screenshot.png)
-->

## Sobre

Comecei isto resolvendo uma lista de exercícios de cadeias de Markov, percebendo que ficava refazendo as mesmas multiplicações de matriz no Excel — uma planilha por problema. A calculadora resolve isso de forma genérica: aceita qualquer matriz `n×n` (de 2 a 10 estados), com rótulos próprios, e responde os tipos de pergunta que aparecem nesses problemas sem que eu precise montar tudo de novo a cada exercício.

No caminho ela cresceu de uma "calculadora de previsão" para uma ferramenta que cobre as principais perguntas sobre cadeias de Markov finitas e de tempo discreto.

## O que ela calcula

| Recurso | Pergunta que responde | Método |
| --- | --- | --- |
| Distribuição por geração | "Qual a distribuição depois de `k` passos?" | `πₖ = π₀ · Pᵏ` |
| Matriz completa por geração | "Para cada estado de partida, onde estarei em `k` passos?" | `Pᵏ` (todas as linhas) |
| Distribuição de equilíbrio | "Para onde o sistema tende no longo prazo?" | Iteração de potência (cadeia regular) |
| Tempo médio de retorno | "A cada quantos passos, em média, volto a este estado?" | `1 / πᵢ` |
| Tempo médio de absorção | "Quantos passos até o processo parar?" | Matriz fundamental `N = (I − Q)⁻¹`, somas de linha |
| Probabilidade de absorção | "Em qual estado final o processo termina, e com que chance?" | `B = N · R` |

A ferramenta **detecta sozinha** se a cadeia tem estados absorventes (linha com `1` na própria diagonal) e troca a análise de equilíbrio pela análise de absorção, que é o que faz sentido nesse caso.

## Funcionalidades

- **Matriz n×n editável** com rótulos de estado personalizáveis.
- **Validação ao vivo**: cada linha mostra um indicador verde quando soma 1 (ou 100%) e vermelho quando não — pega erro de digitação antes do cálculo.
- **Decimal ou porcentagem**: digite `0,7` ou `70`, como estiver no enunciado, e alterne a qualquer momento (a ferramenta converte os valores).
- **Importar / colar matriz**: cole as linhas direto do Excel ou de um PDF (separadas por espaço, vírgula ou tab) e a grade é montada automaticamente, com detecção de decimal vs. porcentagem.
- **Mapa de calor**: as células são tingidas pela magnitude da probabilidade, deixando a estrutura da cadeia visível de relance.
- **Exemplos prontos**: tempo/chuva, transição entre empresas, fluxo de bicicletas e um passeio aleatório com absorção (ruína do jogador) para testar a análise de absorção.
- **Exportar**: botão que copia a tabela ou as matrizes em formato pronto para colar no Excel/Sheets.
- **Tema claro/escuro** e layout responsivo (funciona no celular).

## Como usar

1. Escolha o número de estados e se os valores estão em decimal ou porcentagem.
2. Preencha a matriz de transição — ou cole uma em **Importar / colar uma matriz**.
3. Confira que cada linha soma 1 (indicadores ao lado).
4. Defina a distribuição inicial `π₀`. Os atalhos "começa em X" colocam 100% num único estado, úteis para perguntas do tipo "se chover hoje…".
5. Escolha até qual geração calcular e clique em **Calcular**.

## Convenção matemática

A ferramenta usa matriz **estocástica por linhas**: cada **linha** é o estado de origem e cada **coluna** o estado de destino, de modo que toda linha soma 1. O vetor de estado multiplica a matriz **pela esquerda**:

```
πₖ = π₀ · Pᵏ
```

É a mesma convenção da maioria dos livros-texto em português. Se a sua referência usar matriz estocástica por colunas (`πₖ = Pᵏ · π₀`), basta transpor a matriz antes de digitar.

## Limitações e escopo

Para deixar claro o que a ferramenta cobre — e o que não cobre:

- Trata apenas cadeias **finitas** e de **tempo discreto**.
- A distribuição de equilíbrio é obtida por iteração de potência, então pressupõe uma cadeia **regular**. Cadeias periódicas (que alternam sem assentar) são sinalizadas como "não estabilizou".
- A análise de absorção exige que todo estado transitório consiga **alcançar** algum estado absorvente; se `I − Q` for singular, a ferramenta avisa em vez de devolver número incorreto.
- Suporta de 2 a 10 estados.

## Tecnologia

Arquivo único em HTML, CSS e JavaScript puro (vanilla), **sem nenhuma dependência ou build**. A álgebra linear — multiplicação de matrizes, potências, inversão por eliminação de Gauss-Jordan e a matriz fundamental — é implementada do zero no próprio script. As fontes vêm do Google Fonts por CDN; o resto é tudo local.

Por ser um arquivo só, hospedar é só colocar o `index.html` na raiz de um repositório e ligar o GitHub Pages.

## Autor

Kaike Martins — em transição para análise de dados e BI.
[GitHub](https://github.com/kaike-martins)

---

Sugestões e correções são bem-vindas via *issues*.
