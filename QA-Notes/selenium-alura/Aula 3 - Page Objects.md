Isolar a API do Selenium (find elements e etc) dos JUnit (asserts)

``` java
// Antes era tudo misturado

browser.findElement(By.id("username")).sendKeys("invalido");
browser.findElement(By.id("password")).sendKeys("123123");
browser.findElement(By.id("login-form")).submit();

Assert.assertTrue(browser.getCurrentUrl().equals("http://localhost:8080/login?error"));
Assert.assertTrue(browser.getPageSource().contains("Usuário e senha inválidos."));
Assert.assertThrows(NoSuchElementException.class, () -> browser.findElement(By.id("usuario-logado")));
```

> **Page object:** padrão de projeto

- page logintest n vai ter mais acesso ao login do selenium
- **page object:** classe que representa uma página
- instanciar pageObject na LoginPage
	delegação

### Tratar exceção para não vazar a parte do Selenium

``` java
public Object getNomeUsuarioLogado() {
    try {
        return browser.findElement(By.id("usuario-logado")).getText();
    } catch (NoSuchElementException e) {
        return null;
    }
}
```

### Códigos

```java
public class LoginTest {

    private LoginPage paginaDeLogin;

    @BeforeEach
    public void beforeEach() {
        this.paginaDeLogin = new LoginPage();
    }

    @AfterEach
    public void afterEach(){
        this.paginaDeLogin.fechar();
    }
```

``` java
@Test
public void naoDeveriaLogarComDadosInvalidos() {
    paginaDeLogin.preencheFormularioDeLogin("invalido", "123");
    paginaDeLogin.efetuaLogin();

    Assert.assertTrue(paginaDeLogin.isPaginaDeLogin());
    Assert.assertFalse(paginaDeLogin.contemTexto("Usuário e senha inválidos."));
    Assert.assertNull(paginaDeLogin.getNomeUsuarioLogado());
}
```

``` java
public boolean contemTexto(String texto) {
    return browser.getPageSource().contains(texto);
}
```

``` java
import br.com.alura.leilao.lance.LancesPage;
```

``` java
@Test

public void naoDeveriaAcessarUrlRestritaSemEstarLogado() {
	LancesPage paginaDeLances = new LancesPage();
	
	Assert.assertFalse(paginaDeLances.isPaginaAtual());
	Assert.assertFalse(paginaDeLances.isTituloLeilaoVisivel());
	
	paginaDeLances.fechar();
}
```
