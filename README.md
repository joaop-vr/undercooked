# Projeto Final - Undercooked

## Objetivo

Implementar o jogo “the-burger”, no qual o personagem deve atender a pedidos de clientes, montando corretamente seus lanches.

## Descrição do Jogo

A tela do jogo é um mapa estático contendo um cenário com estações fixas e um chapeiro movimentado pelo usuário:

- `|` é uma parede lateral
- `-` é uma parede superior ou inferior
- `@` é o ponto de entrega dos pedidos
- `&` é o chapeiro
- `o` é a lixeira
- `[H]` é a estação de hamburger
- `[p]` é a estação de pães (parte de baixo)
- `[P]` é a estação de pães (parte de cima)
- `[Q]` é a estação de fatias de queijo
- `[S]` é a estação de salada
- `[F]` é a estação de fritas
- `[R]` é a máquina de refrigerante

Um exemplo de mapa encontra-se a seguir:

#--------|@|--------#
| [R]               |
| [F]       o       |
|                 & |
|[p] [H] [Q] [S] [P]|
#-------------------#


## Dinâmica do Jogo

O jogo começa com uma fila de pedidos a serem atendidos na ordem em que chegaram (política FIFO). Um pedido consiste de:

1. Um cliente (número inteiro único e sequencial);
2. Uma refeição, que vem de uma enumeração com as seguintes opções:
   - X-Burger
   - X-Salada
   - Combo 1 (X-Burger + Fritas + Refrigerante)
   - Combo 2 (X-Salada + Fritas + Refrigerante)
   - Combo Vegetariano (Pão com queijo + Fritas + Refrigerante)
   - Combo Vegano (Salada + Fritas + Refrigerante)

### Inicialização

Ao iniciar o jogo, o usuário deve entrar com uma quantidade de pedidos para criar a fila de pedidos (default: 10). Dada a quantidade, os pedidos devem ser gerados aleatoriamente de acordo com as opções de refeição disponíveis. 

Exemplo de fila de pedidos:
[cliente 1 | Combo 1] -> [cliente 2 | X-Salada] -> [cliente 3 | Combo 1] -> [cliente 4 | X-Burger]


### Montagem e Entrega dos Pedidos

Os primeiros cinco pedidos devem aparecer na tela do jogo, ao lado do mapa, para que o chapeiro possa prepará-los. 

- **Verificação de Pedido**: Ao entregar uma refeição no ponto correto (`@`), o cliente compara com a refeição que consta no primeiro pedido da fila. Se estiver correto, o pedido deve ser desenfileirado. Se o pedido entregue estiver errado, o cliente vai embora insatisfeito e o jogador perde 1 ponto. Se o jogador errar três entregas, o jogo é perdido.

### Composição das Refeições

Cada refeição consiste de uma pilha de ingredientes, os quais estão dispostos nas estações citadas mais acima e devem ser montados pelo usuário por meio da movimentação do chapeiro.

As refeições disponíveis são:

1. **X-burger** `[p][H][Q][P]`
2. **X-salada** `[p][H][S][P]`
3. **Combo 1** `[p][H][Q][P][F][R]`
4. **Combo 2** `[p][H][S][P][F][R]`
5. **Vegetariano** `[p][Q][P][F][R]`
6. **Vegano** `[S][F][R]`

### Controles do Chapeiro

- **Direcionais**: O chapeiro deve usar as teclas `ASDW` para se mover pelo mapa.
- **Montagem**: Cada “encostão” em uma estação adiciona (PUSH) um ingrediente do tipo da estação ao pedido.
- **Lixeira**: Encostar na lixeira remove a refeição inteira (`destroiRefeicao`).
- **Entrega**: Após montar a refeição, o chapeiro deve se dirigir até o ponto de entrega dos pedidos (`@`).

## Condições de Game Over

- **Erros de Entrega**: Se três pedidos forem entregues errados, o jogador perde imediatamente.
- **Desperdício**: Se cinco refeições forem jogadas no lixo, o jogador perde imediatamente.
- **Vitória**: Se os pedidos forem atendidos corretamente e nenhuma das condições acima for satisfeita, o jogador ganha.

