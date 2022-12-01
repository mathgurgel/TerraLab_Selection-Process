# Estratégia de Teste

### Arquitetura 

- Definido pelos desenvolvedores
- Saber tecnologias para testar, dúvidas, coisas não funcionais

### Estratégia de Teste - Escopo

- O que ele abrange/deixa de fora
- Vamos executar que tipo de teste?
- Vai ser executado testes em todos os níveis?
- O que será deixado de fora?
- Será executado testes automatizados?
- Responsabilidade de cada teste
- Lançamento do sistema, como vai ser?

### Ambiente

![[Pasted image 20221201110243.png]]

### Exemplo
```
O plano de testes abrange todas as funcionalidades descritas na tabela acima. Esse plano de testes exclui a funcionalidade de upload de fotos. Serão executados testes em todos os níveis conforme a descrição abaixo:

Testes unitários: o código terá uma cobertura de 60% de testes unitários, que são de responsabilidade dos desenvolvedores.

Testes de integração: serão executados testes de integração em todos os endpoints e esses testes serão de responsabilidade do time de qualidade.

Testes automatizados: serão realizados testes end-to-end na funcionalidade de Login.

Testes manuais: todas as funcionalidades serão testadas manualmente pelo time de qualidade seguindo a documentação de Cenários de teste e deste TestPlan.

Versão beta: será lançada uma versão beta para 20 usuários pré-cadastrados antes do release.
```
