# Projeto_Paradigmas_UFSM

O seguinte projeto é um trabalho da disciplina de paradgmas de programação na Universidade Federal de Santa Maria, o qual os discentes tinham que escolher um tema de projeto e uma linguagem de programação. A proposta de produção individual será de um Mini Banco de dados de Livros e Filmes que recomendará entre um filme e um livro para o usuário e a linguagem utilizada será Prolog. A partir de agora será explicado o código realizado pelo aluno Vitor Mateus Romancini do Amara.

```Prolog
:- use_module(library(random)).
```
Essa linha é uma diretiva é uma diretiva em Prolog que indica ao interpretador SWI-Prolog para carregar o módulo random da biblioteca padrão (library(random)). Isso é feito para que você possa usar as funções e predicados fornecidos por esse módulo que neste caso  fornece funcionalidades relacionadas à geração de números aleatórios como exemplo random/1, que gera um número aleatório, e random_permutation/2, que gera uma permutação aleatória de uma lista.
```Prolog
film("007: Cassino Royale", "Ação").
filme("Cowboys & Aliens", "Ação").
filme("Prenda-me se For Capaz", "Crime").
.....
livro("Dom Casmurro", "Romance").
livro("A Máquina do Tempo", "Ficção Científica").
livro("A Metamorfose", "Ficção Científica").
livro("Os Miseráveis", "Clássico").
....
```

Nestas funções está a base de dados de livros e filmes disponiblizados para o programa escolher para o usuário com o nome e gênero do filme e livro disponíveis. 
```Prolog
gerarRecomendacao(Preferencia, "F") :-
    findall((Titulo, Genero), filme(Titulo, Genero), Filmes),
    gerarRecomendacaoFilme(Preferencia, Filmes, Titulo, Genero),
    write("Recomendação:"), nl,
    write("Título: "), write(Titulo), nl,
    write("Gênero: "), write(Genero), nl.
```
Nesta parte do código é definido as regras para gerar recomendações com base nas preferências do usuário e no tipo de mídia escolhido (filme ou livro). Sendo que na primeira regra tendo o predicado definido como gerarRecomendacao com os argumentos da regra (Preferencia, "F") sendo a preferência do usuário (por exemplo, um gênero) e "F" indica que o usuário deseja uma recomendação de filme.

```Prolog
findall((Titulo, Genero), filme(Titulo, Genero), Filmes),
```
 Esta parte usa o predicado findall para encontrar todos os filmes existentes na base de dados de filmes (filme(Titulo, Genero)) e armazená-los na lista Filmes.
```Prolog
gerarRecomendacaoFilme(Preferencia, Filmes, Titulo, Genero),
```
Chama outra regra chamada gerarRecomendacaoFilme com os argumentos Preferencia, Filmes, Titulo e Genero sendo responsável por selecionar um filme com base na preferência do usuário.
```Prolog
 write("Recomendação:"), nl,
    write("Título: "), write(Titulo), nl,
    write("Gênero: "), write(Genero), nl.
```
Nesta parte o código Escreve "Recomendação:" seguido de uma nova linha na saída, além de "Título:" seguido do título do filme e, em seguida, uma nova linha na saída e "Gênero:" seguido do gênero do filme e, em seguida, uma nova linha na saída.

```Prolog
gerarRecomendacao(Preferencia, "L") :-
    findall((Titulo, Genero), livro(Titulo, Genero), Livros),
    gerarRecomendacaoLivro(Preferencia, Livros, Titulo, Genero),
    write("Recomendação:"), nl,
    write("Título: "), write(Titulo), nl,
    write("Gênero: "), write(Genero), nl.
```
Aqui o código é igual ao discutido acima, no entanto a diferença é que se aplica quando o usuário deseja uma recomendação de livro ("L").
```Prolog
gerarRecomendacao(_, _) :-
    write("Escolha inválida."), nl.
```
Neste caso é quando o usuário escolher algo diferente de "F" ou "L" como tipo de recomendação, a regra "Escolha inválida." será escrita na saída.
```Prolog
gerarRecomendacaoFilme(Preferencia, Filmes, Titulo, Genero) :-
    filtrarFilmes(Preferencia, Filmes, FilmesFiltrados),
    random_member((Titulo, Genero), FilmesFiltrados).
gerarRecomendacaoFilme(_, _, "Não encontramos nenhuma recomendação de filme com base no gênero de sua preferência.", "").

```
Nesta parte vai ser gerada as recomendações de filmes com base nas preferências do usuário com a regra gerarRecomendacaoFilme tendo a responsabilidade de gerar uma recomendação de filme com os argumentos preferencia, filme que é a lista de todos os filmes disponíveis na base de dados e Titulo e Genero que são as variáveis que armazenam o título e o gênero do filme recomendado, respectivamente.


--------------escrever mais esta parte ---------------------


```Prolog
gerarRecomendacaoLivro(Preferencia, Livros, Titulo, Genero) :-
    filtrarLivros(Preferencia, Livros, LivrosFiltrados),
    random_member((Titulo, Genero), LivrosFiltrados).

gerarRecomendacaoLivro(_, _, "Não encontramos nenhuma recomendação de livro com base no gênero de sua preferência.", "").
```

Esta parte é parecida com o código discutido a cima, a diferença é que gera uma recomendação de livro.

```Prolog
filtrarFilmes(Preferencia, Filmes, FilmesFiltrados) :-
    include(filmePertenceAoGenero(Preferencia), Filmes, FilmesFiltrados).

filmePertenceAoGenero(Preferencia, (_, Genero)) :-
    downcase_atom(Genero, GeneroLowerCase),
    downcase_atom(Preferencia, PreferenciaLowerCase),
    sub_atom(GeneroLowerCase, _, _, _, PreferenciaLowerCase).
```

Nesta parte do código ocorre a filtragem de filmes com base na preferência do usuário com a regra filtrarFilmes responsável por filtrar esses filmes com seus argumentos sendo Preferencia, Filmes e FilmesFiltrados que será a lista resultante dos filmes que se encaixam na preferência do usuário.

```Prolog
include(filmePertenceAoGenero(Preferencia), Filmes, FilmesFiltrados).
```
O include/3 é um predicado embutido do Prolog que seleciona elementos de uma lista que satisfazem uma determinada condição, neste caso, a condição é definida pela regra filmePertenceAoGenero(Preferencia), além de FilmesFiltrados conterá todos os filmes da lista Filmes para os quais a regra filmePertenceAoGenero(Preferencia) seja verdadeira.
```Prolog
filmePertenceAoGenero(Preferencia, (_, Genero)) :-
```
Nesta regra verifica se um filme, representado como uma tupla (_, Genero), pertence ao gênero de preferência do usuário
```Prolog
downcase_atom(Genero, GeneroLowerCase),
downcase_atom(Preferencia, PreferenciaLowerCase),
```
A função downcase_atom é usada para converter tanto o Genero quanto o Preferencia em letras minúsculas, tornando a comparação de gêneros case-insensitive.
```Prolog
sub_atom(GeneroLowerCase, _, _, _, PreferenciaLowerCase).
```
A função sub_atom é usado para verificar se o Genero contém o Preferencia. Se a preferência estiver contida no gênero, a regra é verdadeira.
```Prolog
filtrarLivros(Preferencia, Livros, LivrosFiltrados) :-
    include(livroPertenceAoGenero(Preferencia), Livros, LivrosFiltrados).

livroPertenceAoGenero(Preferencia, (_, Genero)) :-
    downcase_atom(Genero, GeneroLowerCase),
    downcase_atom(Preferencia, PreferenciaLowerCase),
    sub_atom(GeneroLowerCase, _, _, _, PreferenciaLowerCase).
```
Nesta parte do código ocorre a filtragem de Livros com base na preferência do usuário igualmente ao código discutido a cima. 
```Prolog
main :-
    write("Bem-vindo ao sistema de recomendação de filmes e livros!"), nl,
    write("Por favor, insira o gênero de filme ou livro que você deseja:"), nl,
    read_line_to_string(user_input, Genero),
    write("Você deseja uma recomendação de filme (F) ou livro (L)?"), nl,
    read_line_to_string(user_input, Escolha),
    gerarRecomendacao(Genero, Escolha).

:- initialization main.

```

Aqui está a parte do código principal do programa main e implementa o ponto de entrada principal do programa e é responsável por interagir com o usuário, coletar suas preferências e gerar recomendações com base nessas preferências. Ele possui os write que escrevem as mensagens ao usuário.  Possui os read_line_to_string(user_input, Genero) e read_line_to_string(user_input, Escolha) que coleta osvalores de entrada de genero e escolha (filme (F) ou livro (L)). 

Por último temos gerarRecomendacao/2 é chamada com base nas preferências coletadas (Genero e Escolha), e o processo de geração de recomendações começa.
```Prolog
:- initialization main.
```
É responsável por iniciar o programa.

A linguagem prolog possui esta facilidade quanto a questão de mexer com base de dados com sua lógica de predicados. 

As referencias para este trabalho foram: 
https://www.ime.usp.br/~slago/slago-prolog.pdf
anotações da professora 

