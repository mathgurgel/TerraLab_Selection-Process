## Aula 2 - Teste do formulário de login

### How to create a selenium test

- add dependencies to `pom.xml`
``` xml
<dependency>

	<groupId>org.seleniumhq.selenium</groupId>

	<artifactId>selenium-chrome-driver</artifactId>

</dependency>
```
- create a class in `src/test/java`
- select the same package of the html page
	ex: `.login (addr/login)`
- create a method
- import `@Test`: `ctrl + shift + o`, first option
``` java
System.setProperty("webdriver.chrome.driver", "drivers/chromedriver.exe");

WebDriver browser = new ChromeDriver();

browser.navigate().to("http://localhost:8080/url");

browser.quit();
```

browser: representa o navegador

`browser.findElement(By.html_attribute`

recomenda-se procurar pelo id
se alguém trocar o id, quebra o teste. é muito frágil.

#### Valid login

``` java
@Test
public void successfulLoginRightInput()
{
	// Set browser
	System.setProperty("webdriver.chrome.driver", "drivers/chromedriver.exe");	
	WebDriver browser = new ChromeDriver();	
	browser.navigate().to("http://localhost:8080/login");
	
	// Fill login form
	browser.findElement(By.id("username")).sendKeys("fulano");	
	browser.findElement(By.id("password")).sendKeys("pass");	
	browser.findElement(By.id("login-form")).submit();
	
	// Make asserts
	Assert.assertFalse(browser.getCurrentUrl().equals("http://localhost:8080/login"));	
	Assert.assertEquals("fulano", browser.findElement(By.id("usuario-logado")).getText());
	
	browser.quit();
}
```

#### Invalid login

```java
@Test
public void naoDeveriaLogarComDadosInvalidos()
{
	browser.findElement(By.id("username")).sendKeys("invalido");
	browser.findElement(By.id("password")).sendKeys("123123");
	browser.findElement(By.id("login-form")).submit();
	
	Assert.assertTrue(browser.getCurrentUrl().equals("http://localhost:8080/login?error"));
	Assert.assertTrue(browser.getPageSource().contains("Usuário e senha inválidos."));
	Assert.assertThrows(NoSuchElementException.class, () -> browser.findElement(By.id("usuario-logado")));
}
```

> selenium quando nao encontra um elemento retorna uma exception

#### Otimizando o código reduzindo redundâncias

``` java
public class LoginTest {
	
    private static final String URL_LOGIN = "http://localhost:8080/login";
    private WebDriver browser;
	
    @BeforeAll
    public static void beforeAll() {
        System.setProperty("webdriver.chrome.driver", "/drivers/chromedriver.exe");
    }
	
    @BeforeEach
    public void beforeEach(){
        this.browser = new ChromeDriver();
        browser.navigate().to(URL_LOGIN);
    }
	
    @AfterEach
    public void afterEach(){
        this.browser.quit();
    }
}
```


### Teste autorização

Não deixar usuário acessar um certo link sem estar logado
> Testar se ele é redirecionado à página de login

```java
@Test
public void naoDeveriaAcessarPaginaRestritaSemEstarLogado() {
    this.browser.navigate().to("http://localhost:8080/leiloes/2");
    Assert.assertTrue(browser.getCurrentUrl().equals("http://localhost:8080/login"));
    Assert.assertFalse(browser.getPageSource().contains("Dados do Leilão"));
}
```

### Conclusão

Nesta aula, aprendemos:

-   Que é possível recuperar elementos na página utilizando o método `findElement()`;
-   Que é possível recuperar o código fonte da página utilizando o método `getPageSource()`;
-   Que é possível recuperar o url atual do browser utilizando o método `getCurrentUrl()`;
-   Que devemos utilizar o método `sendKeys()` para enviar textos para os `inputs` da página;
-   Que uma das maneiras de submeter um formulário é via método `submit()`.