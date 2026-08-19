Divisão por Desenvolvedor

Gustavo Ramos: Fundação e Estado Físico
Requisitos: 01 (Regras Gerais) + 02 (Energia) + 06 (Higiene)

Testes sob responsabilidade:
* Deve conseguir criar um novo Cresim com nome, pontos de higiene e energia carregados e 1500 Cresceleons
* Deve conseguir atribuir uma aspiração ao Cresim
* Deve validar os pontos de energia do personagem para que não passem de 32 pontos
* Deve validar os pontos de energia do personagem para que não fiquem negativados
* Deve conseguir dormir e receber seus pontos de energia
* Deve descontar 10 Cresceleons ao tomar banho

Foco: Construir a classe/molde do Cresim, validações de atributos físicos (energia/higiene), criação de personagem, sono e banho.
Por que agrupar: Energia e higiene são atributos base do Cresim criado no Req 01. Quem controla a criação do personagem deve controlar as regras de validação dos atributos físicos para expor uma interface estável aos outros devs.

Henrique Araújo: Progressão e Economia
Requisitos: 03 (Habilidades e Aspirações) + 04 (Trabalho)

Testes sob responsabilidade:
* Deve conseguir comprar um item de habilidade
* Deve validar ao tentar comprar um item de habilidade sem Cresceleons suficientes
* Deve conseguir concluir um ciclo de treino com habilidade que não é aspiração e receber os pontos corretamente
* Deve conseguir concluir um ciclo de treino com habilidade que é sua aspiração e receber os pontos corretamente
* Deve perder pontos de energia ao terminar um ciclo de treino
* Deve perder pontos de higiene ao terminar um ciclo de treino
* Deve avançar o nivel de habilidade quando completar os pontos necessarios
* Deve perder os pontos de energia ao trabalhar uma jornada padrão
* Deve receber o salario do dia ao trabalhar uma jornda padrão
* Deve receber o salario equivalente quando começar a trabalhar com os pontos de energia menores que 10
* Deve receber o salario equivalente quando começar a trabalhar com os pontos de energia menores que 10 e pontos de higiene menores que 4
* Deve validar para que o Cresim não consiga começar a trabalhar com os pontos de energia menores que 4

Foco: Sistema de itens, treino, evolução de níveis (Júnior/Pleno/Sênior), empregos e recálculo de salário.
Por que agrupar: O salário do trabalho depende diretamente do nível de habilidade do Cresim. Além disso, tanto treino quanto trabalho consomem energia e higiene. Ficando com a mesma pessoa, fica mais fácil testar o consumo desses atributos em ações produtivas sem depender de outro dev.

Lorenzo: Social e Comandos Especiais
Requisitos: 05 (Relacionamentos) + 07 (Cheats)

Testes sob responsabilidade:
* Deve evoluir o relacionamento de dois Cresims para AMIZADE
* Deve recuar o relacionamento de dois Cresims para INIMIZADE
* Deve descontar os pontos de energia em uma interação entre dois Cresims
* Deve conseguir aplicar o cheat SORTENAVIDA e receber as recompensas
* Deve conseguir aplicar o cheat DEITADONAREDE e receber as recompensas
* Deve conseguir aplicar o cheat TERAPIA e receber as recompensas
* Deve conseguir aplicar o cheat DESODORANTE e receber as recompensas
* Deve conseguir aplicar o cheat WHEYPROTEIN e receber as recompensas
* Deve conseguir aplicar o cheat SINUSITE e ter a vida zerada

Foco: Interações entre Cresims, evolução de relacionamento (Neutro/Amizade/Amor/Inimizade) e processamento de todos os cheats.
Por que agrupar: O cheat TERAPIA afeta diretamente os pontos de relacionamento. Manter cheats e relacionamentos juntos evita que Lorenzo precise depender de outra pessoa para testar o cheat social. Os demais cheats manipulam atributos já expostos pelo Gustavo Ramos (energia, higiene, vida, dinheiro).

Estrutura sugerida do src:

Como o index.js fica na raiz e os testes ficam em __tests__, a pasta src pode seguir este padrão modular:

```
src/
    models/
        Cresim.js
    services/
        coreService.js
        energiaService.js
        higieneService.js
        habilidadeService.js
        trabalhoService.js
        relacionamentoService.js
        cheatService.js
    utils/
        validacoes.js
    config/
        constants.js
```

Observação sobre dependências:
* O Gustavo Ramos deve priorizar a entrega do modelo Cresim e dos métodos de get/set de energia/higiene, pois Henrique Araújo e Lorenzo precisarão consumir essa interface.
* O Henrique Araújo precisará consultar o nível de habilidade do Cresim para calcular o salário. Por isso faz sentido que habilidades e trabalho fiquem juntos.
* O Lorenzo pode trabalhar de forma mais independente, apenas consumindo a lista de Cresims existentes e os métodos de energia do Gustavo Ramos.