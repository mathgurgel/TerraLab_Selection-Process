## Aula 5 - AJAX e Boas Práticas

### Teste de requisições assíncronas

- Códigos javascript podem ser demorados, demorando pra carregar e impossibilitando testar certos elementos da página (element not found). ex: Ajax

> Mandar Selenium esperar um tempo antes de lançar um erro

```java
this.browser.manage().timeouts().implicitlyWait(5, TimeUnit.SECONDS);
```

### Guideline de boas práticas

[link](https://www.selenium.dev/documentation/test_practices/encouraged/)

- Criar métodos com nomes legíveis baseados no domínio de aplicação
- Não preparar páginas com o Selenium. Preparar nos próprios cenários de teste
- Se o aplicativo deve acessar um serviço externo, faça um _mock_. (mockito no Java).
- JUnit: report de testes usando Maven
- Evitar compartilhar estado entre cenários de teste.
- Cada teste deve rodar de maneira independente
- Encaminhamento de métodos para legibilidade [(here)](https://www.selenium.dev/documentation/test_practices/encouraged/consider_using_a_fluent_api/)
- Cada teste deve ter um navegador limpo (Fresh browser per test). Abrir e fechar navegador para evitar compartilhar cookies, cache, etc.

### Conclusão

- Teste de aceitação (end-to-end, UI)
- **driver**: possibilita selenium conversar com o browser
- pageObjects
- guidelines