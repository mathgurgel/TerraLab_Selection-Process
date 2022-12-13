# Sprint 3 - BDD - Histórias de Usuário & Cenários de Teste (framework)

Matheus Neto Gurgel

## **Título:** Adicionar pontos e visualizar endereços no mapa

### História do usuário:

**EU COMO** usuário cadastrado

**GOSTARIA DE** poder inserir um ponto no mapa

**PARA que** eu possa visualizar um endereço no mapa

### Cenário de teste:

**Dado** que eu estou na [tela inicial](https://inteligenciageografica-a377d.web.app/) do software Terralab,
**Quando** eu clicar no botão de menu `"button-controlhud"`
**E** eu clicar no botão _Rotas_ `"button-menu-route"`
**E** eu clicar no botão _Add ponto_ `"button-add-routes"`
**E** eu inserir um ponto de coordenadas referente a um endereço na caixa de texto `""`
**E** eu clicar no botão de confirmar `""`,
**Então** devo ser redirecionado ao local do mapa referente ao meu endereço.

## Extra

## Título: buscar endereços para visualização no mapa

### História do usuário

**EU COMO** usuário cadastrado

**GOSTARIA DE** inserir um endereço

**PARA que** eu possa visualizar um endereço no mapa

### Cenário de Teste

**Dado** que eu estou na [tela inicial](https://inteligenciageografica-a377d.web.app/) do software Terralab,
**Quando** eu digitar um endereço no campo de busca `"input-field-search"`
**E** eu clicar com o botão esquerdo do mouse em cima do endereço sugerido (`"search-result-X-autocomplete"`),
**Então** devo ser redirecionado ao local do mapa referente ao meu endereço.



