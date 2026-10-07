# Demonstação - Hash_ID - Rafael Duarte

## Sobre o projeto
O Hash_ID é uma ferramenta em Python que sugere possíveis algoritmos
de hash a partir de prefixos, comprimento e caracteres da entrada.
Os resultados incluem candidatos, pontuação de confiança e justificativa.

## Funcionalidades
A versão entregue permite entrada pelo terminal, arquivo ou stdin,
saída em JSON, indicação de modos do hashcat e classificação de
campos separados por `:`. Também reconhece alguns formatos que
não são hashes e apresenta uma estimativa simplificada de
dificuldade de quebra.

## Resultados e validações
Nos exemplos demonstrados, a ferramenta identificou:

- Testes (`just test`): 69/69 testes passaram.
- Análise estática (`just lint`): Todos os checks passaram e código avaliado em 10/10.
- Validação dos hases de demonstração:
    - `5f4dcc3b5aa765d61d8327deb882cf99`
    - `e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855`
    - `$2b$12$EixZaYVK1fsbw1ZfbX3OXePaWxn96p36WQNQy.uK4Of2T7G.VHvgvWK`
    - `$argon2id$v=19$m=65536,t=3,p=4$c29tZXNhbHQ$RdescudvJCsgt3ub+b+dWRWJTmaaJObG`
    - `$apr1$JlOdSlVe$ipa1mTAv3LFRBHHzqaIaH/`
    - `*A4B6157319038724E3560894F7F932C8886EBFCF`
    - `eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIn0.dozjgN...`

    Resultados respectivos:
    - MD5 (0.60) | 32 caracteres hex — candidato mais provável para este comprimento
    - SHA-256 (0.60) | 64 caracteres hex — candidato mais provável para este comprimento
    - bcrypt (0.95) | prefixo `$2b$` — string PHC bcrypt, variante 2b (atual)
    - Argon2id (0.95) | prefixo `$argon2id$` — string PHC moderna, o padrão atual
    - Apache MD5-crypt (0.95) | prefixo `$apr1$` — variante MD5 do Apache htpasswd (`htpasswd -m`)
    - MySQL5 (0.85) | começa com `*` seguido por 40 caracteres hex maiúsculos
    - JWT (não é um hash) (0.30) | prefixo `eyJ` é o base64 de `{"` — JWT, não é um hash

## Decisões e conclusões
A identificação prioriza prefixos conhecidos e utiliza comprimento
e caracteres quando não encontra um prefixo correspondente.
Como diferentes algoritmos podem ter o mesmo formato de saída,
a ferramenta apresenta candidatos em vez de garantir uma identificação.

Com o projeto, aprendi o que são hashes, seus principais tipos e como funcionam sistemas de validações, além de como lidar com entradas via comando do terminal.
Uma possível melhoria seria validar com mais rigor a estrutura
dos formatos reconhecidos e adicionar mais algoritmos.

## Vídeo
[Vídeo de demonstração](https://youtu.be/me0ok_lFsOg)