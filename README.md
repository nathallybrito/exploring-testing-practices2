# Explorando Práticas de Teste

Neste exercício, vamos explorar práticas de teste em sistemas reais utilizando a ferramenta [TestMiner](https://andrehora.github.io/testminer).

O TestMiner permite visualizar e analisar testes de software em repositórios do GitHub, fornecendo dados sobre como os projetos organizam seus testes, como eles evoluem entre versões e quais bibliotecas de teste são utilizadas.
Explore a ferramenta antes de começar para se familiarizar com seu funcionamento.

Mais detalhes no GitHub da ferramenta: https://github.com/andrehora/testminer.

---

## Passo 1: Selecionar DOIS repositórios

Escolha dois repositórios reais que possuam testes de software.
Abaixo estão alguns links para ajudá-lo a encontrar projetos interessantes:

- Python: https://github.com/topics/python?l=python
- JavaScript: https://github.com/topics/javascript?l=javascript
- TypeScript: https://github.com/topics/typescript?l=typescript
- Java: https://github.com/topics/java?l=java

- Tópicos: [ai](https://andrehora.github.io/testminer/#topic:ai), [llm](https://andrehora.github.io/testminer/#topic:llm), [api](https://andrehora.github.io/testminer/#topic:api), [nodejs](https://andrehora.github.io/testminer/#topic:nodejs), [android](https://andrehora.github.io/testminer/#topic:android)

- Por organização: [Google](https://andrehora.github.io/testminer/#google), [Microsoft](https://andrehora.github.io/testminer/#microsoft), [Apple](https://andrehora.github.io/testminer/#apple), [Facebook](https://andrehora.github.io/testminer/#facebook), [Netflix](https://andrehora.github.io/testminer/#netflix), 
[GitHub](https://andrehora.github.io/testminer/#github), [Apache](https://andrehora.github.io/testminer/#apache), [HuggingFace](https://andrehora.github.io/testminer/#huggingface)

## Passo 2: Explorar os repositórios selecionados

Busque os repositórios escolhidos no [TestMiner](https://andrehora.github.io/testminer) e analise os dados de teste gerados pela ferramenta.

## Passo 3: Explicar as prática de teste

Para cada repositório, escolha uma prática ou dado de teste relevante e explique com suas próprias palavras.

---

## Instruções de entrega

1. Faça um `fork` deste repositório (saiba mais sobre forks [aqui](https://docs.github.com/pt/pull-requests/collaborating-with-pull-requests/working-with-forks/fork-a-repo)).
2. Responda às questões abaixo diretamente neste arquivo `README.md` do seu fork. Pode adicionar imagens para enriquecer sua explicação.
3. No Moodle, submeta apenas a URL do seu fork.

---

## Respostas

### Repositório 1 
Repositório: `https://github.com/facebook/react`

URL TestMiner: `https://andrehora.github.io/testminer/#facebook/react`

Explicação: Ao analisar o repositório do React no TestMiner, a prática de teste mais marcante é a **co-localização de testes** associada ao uso maciço do framework **Jest** (desenvolvido pela própria equipe do Facebook). 

Em vez de centralizar todos os testes em um único diretório raiz distante do código-fonte, a arquitetura do React adota a estratégia de manter os testes fisicamente próximos aos arquivos de implementação. Os testes geralmente ficam em diretórios `__tests__` espalhados por todo o projeto ou levam sufixos como `-test.js` logo ao lado do componente que estão testando.

**Por que essa prática é relevante e o que os dados mostram:**
*   **Redução da Carga Cognitiva:** Quando um desenvolvedor vai alterar o funcionamento de um componente, o arquivo de teste está imediatamente visível na mesma pasta. Isso estimula a atualização imediata dos testes e facilita a refatoração.
*   **Escalabilidade em Projetos Massivos:** Em monorepos ou projetos de grande escala como o React, uma pasta `/tests` global se tornaria um labirinto caótico. A co-localização divide a complexidade, organizando os testes por contexto de domínio.
*   **Crescimento Linear:** O gráfico temporal no TestMiner demonstra que o volume de código de teste cresce de forma perfeitamente alinhada com o código de produção. Isso evidencia a existência de uma esteira de Integração Contínua (CI) rigorosa, onde nenhuma funcionalidade (Pull Request) é aceita sem a respectiva cobertura de testes (regressão e unidade), garantindo que atualizações não quebrem aplicações ao redor do mundo.

---
### Repositório 2

Repositório: `https://github.com/pallets/flask`

URL TestMiner: `https://andrehora.github.io/testminer/#pallets/flask`

Explicação: Explorando o repositório do Flask (um dos microframeworks Python mais populares) no TestMiner, destaca-se a prática de **separação estrutural estrita** apoiada pelo motor de testes **pytest**.

Em contraste direto com a abordagem do React, o Flask segue a convenção clássica do ecossistema Python: existe uma fronteira física clara entre o código da aplicação e o código de verificação. Todo o núcleo do framework reside em diretórios de código-fonte (como `src/flask`), enquanto a suíte de testes inteira é centralizada em um diretório raiz exclusivo chamado `tests/`.

**Por que essa prática é relevante e o que os dados mostram:**
*   **Isolamento para Empacotamento:** O Flask é uma biblioteca distribuída via PyPI (Python Package Index). Separar fisicamente os testes garante que, quando um usuário instala o framework em seu servidor, ele não faça o download de megabytes de dados de teste desnecessários para a execução em produção.
*   **Poder de Simulação (Fixtures):** A centralização favorece o uso de *fixtures* do `pytest` (arquivos `conftest.py` na raiz da pasta de testes). Isso permite criar simulações de servidores web, contextos de requisição e bancos de dados em memória que podem ser reutilizados por todos os testes de integração do projeto.
*   **Estabilidade de API Pública:** O histórico de evolução do TestMiner revela que a equipe foca pesadamente em testes de contrato e integração. Os picos de aumento de testes geralmente coincidem com novas *tags* de versão. Como o Flask serve de base para milhares de outras aplicações, a garantia de retrocompatibilidade através de uma suíte centralizada que testa o comportamento externo das APIs é tratada como prioridade máxima.