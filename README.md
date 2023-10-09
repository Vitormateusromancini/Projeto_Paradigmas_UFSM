# Projeto_Paradigmas_UFSM

O seguinte projeto é um trabalho da disciplina de paradgmas de programação na Universidade Federal de Santa Maria, o qual os discentes tinham que escolher um tema de projeto e uma linguagem de programação. A proposta de produção individual será de um Mini Banco de dados de Livros e Filmes que recomendará entre um filme e um livro para o usuário e a linguagem utilizada será Prolog. A partir de agora será explicado o código realizado pelo aluno Vitor Mateus Romancini do Amara.

```Prolog
:- use_module(library(random)).
```
Essa linha é uma diretiva é uma diretiva em Prolog que indica ao interpretador SWI-Prolog para carregar o módulo random da biblioteca padrão (library(random)). Isso é feito para que você possa usar as funções e predicados fornecidos por esse módulo que neste caso  fornece funcionalidades relacionadas à geração de números aleatórios como exemplo random/1, que gera um número aleatório, e random_permutation/2, que gera uma permutação aleatória de uma lista.
