## Aula 4 - Carregando o formulário de cadastro de leilão

`ctrl + shift + r`: renomeia tudo de uma vez (ctrl d pro arquivo inteiro)

``` java
public LeiloesPage efetuaLogin() {
    browser.findElement(By.id("login-form")).submit(); // já redireciona a página
    return new LeiloesPage(browser); // continuar na mesma página, passa o webdriver
}
```

``` java
// construtor
public LeiloesPage(WebDriver browser) {

    System.setProperty("webdriver.chrome.driver", "/drivers/chromedriver.exe");
    this.browser = browser;
}
```

`ctrl + u`: cria método na classe a partir de código em outra que está o usando

```java
public void deveriaCadastrarLeilao() {
    LoginPage paginaDeLogin = new LoginPage();
    paginaDeLogin.preencheFormularioDeLogin("fulano", "pass");
    this.paginaDeLeiloes = paginaDeLogin.efetuaLogin();
    CadastroLeilaoPage paginaDeCadastro = paginaDeLeiloes.carregarFormulario();

    String hoje = LocalDate.now().format(DateTimeFormatter.ofPattern("dd/MM/yyyy"));
    String nome = "Leilao do dia " + hoje;
    String valor = "500.00";

    this.paginaDeLeiloes = paginaDeCadastro.cadastrarLeilao(nome, valor, hoje);
    Assert.assertTrue(paginaDeLeiloes.isLeilaoCadastrado(nome, valor, hoje));

}
```

```java
public boolean isLeilaoCadastrado(String nome, String valor, String data) {
    WebElement linhaDaTabela = this.browser.findElement(By.cssSelector("#tabela-leiloes tbody tr:last-child"));
    WebElement colunaNome = linhaDaTabela.findElement(By.cssSelector("td:nth-child(1)"));
    WebElement colunaDataAbertura = linhaDaTabela.findElement(By.cssSelector("td:nth-child(2)"));
    WebElement colunaValorInicial = linhaDaTabela.findElement(By.cssSelector("td:nth-child(3)"));

    return colunaNome.getText().equals(nome)
            && colunaDataAbertura.getText().equals(data) 
            && colunaValorInicial.getText().equals(valor);
}
```

O método `findElement` devolve um objeto do tipo `WebElement`, que pode ser atribuído a uma variável.

### Teste de validações (de entrada)

Quando o usuário digitar um input errado, deveria aparecer mensagens dizendo o que ele fez de errado.

```java
@BeforeEach
public void beforeEach() {
    LoginPage paginaDeLogin = new LoginPage();
    paginaDeLogin.preencheFormularioDeLogin("fulano", "pass");
    this.paginaDeLeiloes = paginaDeLogin.efetuaLogin();
    this.paginaDeCadastro = paginaDeLeiloes.carregarFormulario();
}
```

```java
public boolean isPaginaDeValidacaoVisiveis() {
    String pageSource = browser.getPageSource();
    return pageSource.contains("minimo 3 caracteres")
            && pageSource.contains("não deve estar em branco")
            && pageSource.contains("deve ser um valor maior de 0.1")
            && pageSource.contains("deve ser uma data no formato dd/MM/yyyy");
}
```

```java
@Test
public void deveriaValidarCadastroDeLeilao() {
	this.paginaDeLeiloes = paginaDeCadastro.cadastrarLeilao("", "","");
	Assert.assertFalse(this.paginaDeCadastro.isPaginaAtual());
	Assert.assertTrue(this.paginaDeLeiloes.isPaginaAtual());
	Assert.assertTrue(this.paginaDeCadastro.isPaginaDeValidacaoVisiveis());
}
```

**Testar se está na página**

```java
public boolean isPaginaAtual() {
	return browser.getCurrentUrl().equals(URL_LEILOES);
}
```


![[Pasted image 20221212173923.png]]

### Organizando o código

- Eliminar repetições de loginpage, lancespages, etc

#### Criar uma superclasse e herdar dela

```java
public class PageObject {

    protected WebDriver browser;

    public PageObject(WebDriver browser) {
        System.setProperty("webdriver.chrome.driver", "/drivers/chromedriver.exe");
        if (browser == null) {
            this.browser = new ChromeDriver();
        } else {
            this.browser = browser;
        }
    }

    public void fechar() {
        this.browser.quit();
    }
}
```

Loginpage:
```java
public class LoginPage extends PageObject {

    private static final String URL_LOGIN = "http://localhost:8080/login";

    public LoginPage() {
        super(null);
        browser.navigate().to(URL_LOGIN);
    }
```

CadastroLeilaoPage:
```java
public class CadastroLeilaoPage extends PageObject {

    private static final String URL_CADASTRO_LEILAO = "http://localhost:8080/leiloes/new";

    public CadastroLeilaoPage(WebDriver browser) {
        super(browser);
    }
```

> chamar construtor de classe pai no java: `super(browser)`

