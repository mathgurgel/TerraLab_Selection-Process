# Sprint 4 - Qualidade de Software como Serviço (SaaS)

Matheus Neto Gurgel

## Selenium

Nessa Sprint, foi concluído o curso da Alura de Selenium, uma ferramenta para automatização de testes de UI/aceitação/end-to-end.  
As anotações do curso, para cada aula, se encontram [aqui](https://github.com/mathgurgel/TerraLab_Selection-Process/tree/main/QA-Notes/selenium-alura).  

### Desafio

Com base em um software bem conhecido, o [SIG](https://inteligenciageografica-a377d.web.app/), criar um teste para uma
funcionalidade específica das áreas de back-end e front-end.

#### Front-end

```
Front-End: Teste de Aceitação para o Serviço Pesquisa de Ponto no mapa a
partir de endereço (Utilize a história de usuário fornecida e o cenário de teste
desenvolvido anteriormente).
```

Para isso, foi criado os seguinte métodos:  
```java
public void searchAddress(String endereco) {
	browser.findElement(By.id("input-field-search")).sendKeys(endereco);
	browser.findElement(By.id("button-search-input-field-search")).click();
}
```

```java
public boolean isTherePoint() {
	WebElement foo = new WebDriverWait(browser, Duration.ofSeconds(10))
	.until(browser -> browser.findElement(By.className("pin-input-field-search")));
	return browser.getPageSource().contains("pin-input-field-search");
}
```

```java
@Test
public void shouldAddAPointByAddress() {
	searchPointPage.searchAddress("ouro preto");
	Assert.assertTrue(searchPointPage.isTherePoint());
}
```

No entanto, ao realizar os testes, o botão de pesquisar não estava, de fato, sendo clicado. O botão estava até, de uma certa maneira, sendo selecionado pelo Selenium, porém o clique simulado com o botão esquerdo do mouse, não foi efetuado.  

Para contornar isso, tentei algumas alternativas:

```java
// Tentando fazer o clique usando Actions
WebElement clickable2 = browser.findElement(By.id("button-search-input-field-search"));
new Actions(browser)
	.doubleClick(clickable2)
	.perform();
```

```java
// Utilizando uma "espera" para o botão ser clicável
WebElement firstResult = new WebDriverWait(browser, Duration.ofSeconds(1000))
	.until(ExpectedConditions.elementToBeClickable(By.id("button-search-input-field-search")));

// firstResult.click();
```

```java
// Clicando em outro canto da página antes de clicar no botão de pesquisa
WebElement clickable2 = browser.findElement(By.id("button-search-input-field-search"));
new Actions(browser)
	.doubleClick(clickable2)
	.perform();
```

Porém, nada disso funcionou.  
Já utilizando esperas e clicando no botão manualmente, o JUnit test rodou sem problemas.

#### Back-End

##### Unit

```
Testes Unitários para o Serviço de Mapeamento de Respostas das
APIs do Componente GeoCrawler (Dica: Utilize o conceito de Mock
Functions).
```

Li os artigos referentes à documentação do Jest, no entanto, ao rodar o comando `npx prisma db pull --schema=./src/infra/db/techs/prisma/config/schema.prisma`, ocorreu os seguintes erros:  

```
Error: Get config: Schema Parsing P1012

error: Environment variable not found: DATABASE_URL.
```


##### Functional

```
Testes Funcionais para o Serviço de Gerenciamento de Projetos do
Componente Qgis Server.
```

Os artigos referentes ao Pytest foram lidos, porém, ao rodar o componente, o seguinte erro ocorreu:  
```
Error response from daemon: Head "http://ip/v2/servidor-de-dados-geograficos/manifests/stable": no basic auth credentials
```

### Disclaimer

Com esses erros, mesmo recorrendo a ajudas, não foi possível implementar todos os testes a tempo da sprint.


