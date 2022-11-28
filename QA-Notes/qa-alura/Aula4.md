# Pirâmide de Testes

### Teste de caixa preta

Consegue fazer o teste sem saber a implementação

### Teste de caixa brancha

É necessário saber a implementação

## Pirâmide

![[Pasted image 20221125170844.png]]

Fazer mais unitário, depois service e o minimo de UI.
UI tende a mudar com bastante frequência
Automatizar testes de serviço e fazer muitos unitários

```
Na base da pirâmide ficam os testes da menor parte testável de uma aplicação, aqueles que testam a classe ou uma função dentro do código, ou seja, os testes de unidade.

No meio, os testes de integração, que testam como diferentes módulos do sistema interagem entre si, como os de comunicação entre serviços, comunicação com bancos de dados e assim por diante.

No topo, teremos os testes de ponta a ponta que buscam testar todo o fluxo de funcionamento da aplicação.
```

### Gravador de passos no Windows

Programa utilizado para registrar testes (prints por eventos)

`Windows + R + "psr"`

[Por quê e o que é possível testar](https://www.alura.com.br/artigos/por-que-e-o-que-e-possivel-testar)

