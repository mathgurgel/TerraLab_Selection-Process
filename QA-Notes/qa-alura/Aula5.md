# Gestão de Erros

### Defeito X Falha

Defeito: erro num código ou documento
Falha: manifestação do defeito.

## Bug

Comportamento indesejado
**Prevenir**, quanto mais cedo achar, melhor.

Dúvidas podem gerar comportamentos inesperados no futuro. Ex: quem comentar o post vai ser identificado como?
> Deve ser exibido o nome do usuário

### Report de bugs

Bug tracker;
Jira

Reproduzir o bug 3x para ter certeza do procedimento que leva a ele.

### Severidade dos bugs

É definida pelo QA

- Blocker (Crítico): inibe de avançar o sistema
- Grave: não funciona como o esperado/especificado.
- Moderada: feature que não tem tudo especificado, porém de menor impacto.
- Pequeno: erro ortográfico, visual, não impacta em nada no funcionamento

### Prioridade dos bugs

- Definida pelo líder do processo.
- Depende se a funcionalidade é relevante ou não. Exemplo: cliente considera login mais importante do que o botão de curtir, mesmo que a severidade do botão de curtir seja maior.

### Report de bugs

#### Resumo

Um bom resumo deve colaborar para quem o leia, identifique o erro rápido. Evitar sugerir soluções

**Exemplo:** Ao cadastrar usuário, sistema não redireciona para login.

#### Descrever passos precisos para reprodução do erro

Descreva a interação com o sistema, de maneira clara.

**Exemplos:**
- **Impreciso:** "Abra o sistema."
- **Preciso:** "Pressione `Cmd+N` para abrir uma nova janela no navegador. Em seguida, digite `https://alurapic.com.br/ na barra de endereço` e tecle `Enter`."
- **Impreciso:** "Preencha o Cadastro."
- **Preciso:** "Na tela de cadastro, digite usuário, e-mail, senha, confirme a senha e clique em `Cadastrar`.”
- **Impreciso:** "Não funciona."
- **Preciso:** Ao Clicar em `Cadastrar`, o sistema permanece estático, não dá feedback ao usuário e permanece na tela de `Cadastro`."

#### Outras informações

- **Versão:** Qual versão do produto você está testando?
- **Plataforma:** Mencione a plataforma de hardware em que foi encontrado o bug. São várias as plataformas como “PC”, “MAC”, “IOS”, “Android” e etc.
- **Navegador:** Qual browser você usou para testar. No meu caso, usei o Google Chrome.
- **Screenshot** da tela com o código de erro.