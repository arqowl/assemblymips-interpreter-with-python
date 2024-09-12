# Documentação do Interpretador de Assembly da disciplina de Paradigmas de linguagem de programação

## 🤝 Colaboradores
- [Arquimedes](https://github.com/arqowl)
- [Gil](https://github.com/Gil32610)

## Contextualização
- O problema do jantar dos filósofos é um clássico na área de concorrência, parte fundamental da programação paralela e distribuída. Foi proposto por Edsger Dijkstra para ilustrar os desafios de sincronização e evitar deadlocks em sistemas paralelos. A ideia é a seguinte:
      1. Cinco filósofos estão sentados ao redor de uma mesa circular. Cada filósofo alterna entre comer e pensar. Para comer, eles precisam pegar dois garfos (um de cada lado do prato). No entanto, só há cinco garfos, então eles precisam coordenar entre si para evitar situações onde todos pegam um garfo e ficam esperando eternamente pelo outro (o que levaria a um deadlock).

## Perspectiva na programação paralela e distribuída
    1. *Concorrência:* Cada filósofo representa uma thread ou processo que compete por recursos compartilhados (os garfos). No contexto de programação paralela, esses processos precisam acessar os recursos de forma sincronizada para evitar problemas como condições de corrida, onde múltiplos processos tentam acessar o mesmo recurso ao mesmo tempo.
    2. *Problemas Clássicos:*
        - `Deadlock:` Se cada filósofo pegar um garfo e esperar pelo outro, ninguém conseguirá comer. Esse é o deadlock, uma situação onde todos os processos ficam presos esperando por recursos que nunca serão liberados. Em sistemas distribuídos, deadlock pode ocorrer quando diferentes nós ou processos aguardam indefinidamente pela liberação de recursos compartilhados.
        - `Starvation (Inanição):` Mesmo que o deadlock seja evitado, um ou mais filósofos podem nunca conseguir comer se os outros sempre pegarem os garfos antes deles. Em um sistema distribuído, isso ocorre quando certos processos ou nós têm prioridade menor ou são constantemente preteridos, levando a ineficiência.

## Nossa Solução
    1. *Locks e Synchronized*
O uso de locks e do modificador synchronized em linguagens como Java é uma abordagem comum para gerenciar o acesso de múltiplas threads a recursos compartilhados, como os garfos no problema dos filósofos. O conceito de exclusão mútua (mutual exclusion) é central aqui.
        - `Como funciona:` Cada filósofo (ou thread) tenta pegar dois garfos (recursos). Para garantir que dois filósofos não peguem o mesmo garfo ao mesmo tempo, usamos locks. Em Java, isso pode ser implementado com o modificador synchronized. Quando um filósofo pega um garfo (ou entra em uma região crítica), ele adquire um lock sobre esse garfo, e nenhuma outra thread pode acessar esse recurso até que o lock seja liberado.

    2. *Troca de Mensagens (Composite Pattern)*
A troca de mensagens é uma abordagem comum em sistemas distribuídos. Ao invés de ter threads ou processos compartilhando recursos diretamente (como os garfos), eles trocam mensagens para coordenar suas ações. Isso é útil quando se trabalha com múltiplos nós em sistemas distribuídos.
     - `Como funciona:` Em vez de filósofos competirem diretamente pelos garfos, eles enviam mensagens solicitando e liberando recursos. Cada filósofo comunica suas intenções de pegar um garfo ou devolvê-lo. Essa abordagem é escalável e evita deadlocks, pois pode ser feita em um ambiente totalmente distribuído, onde cada recurso é gerido por um nó separado.

    3. *Wait/Notify (ou Wait/Signal)*
O uso de wait() e notify() (ou notifyAll()) é outra maneira eficiente de coordenar threads em ambientes de concorrência, particularmente em situações onde uma thread precisa aguardar até que um recurso esteja disponível.

- `Como funciona:` Um filósofo só pode comer quando os dois garfos estão disponíveis. Se um dos garfos não estiver disponível, o filósofo pode chamar wait() para liberar a CPU até que o garfo fique disponível (ou seja, até que outra thread libere o garfo). Quando um filósofo termina de comer e devolve os garfos, ele pode chamar notify() ou notifyAll() para acordar as threads que estavam esperando por esses recursos.
