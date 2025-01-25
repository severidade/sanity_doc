# Configuração do Sanity.io em um Projeto React

Este guia apresenta os passos necessários para configurar o Sanity.io em um projeto React.

---

## 1. Configuração da Conexão Local com o Banco de Dados Sanity

### Criação do Arquivo de Configuração

1. Dentro da pasta `src`, crie um arquivo chamado `client.js`. Este arquivo será responsável por configurar a conexão com o banco de dados Sanity.

2. No arquivo `client.js`, importe o módulo `sanityClient` do pacote `@sanity/client` e exporte uma instância do cliente Sanity com as configurações apropriadas. Certifique-se de definir `useCdn` como `true` se desejar buscar no cache do edge e especifique a `apiVersion` como a data atual (`YYYY-MM-DD`) para segmentar a versão mais recente da API.

```javascript
import sanityClient from '@sanity/client';

export default sanityClient({
  projectId: 'SEU_PROJECT_ID',
  dataset: 'SEU_DATASET',
  useCdn: true,
  apiVersion: 'YYYY-MM-DD',
});
```

Substitua `SEU_PROJECT_ID` e `SEU_DATASET` pelos valores apropriados encontrados em `sanity.cli.js`.

---

## 2. Instalação das Dependências

Na raiz do seu projeto, execute os seguintes comandos no terminal para instalar as dependências necessárias:

```bash
npm install @sanity/client
npm install @sanity/block-content-to-react
```

- **`@sanity/client`**: Biblioteca para conectar sua aplicação React ao Sanity.io.
- **`@sanity/block-content-to-react`**: Biblioteca para renderizar conteúdo estruturado do Sanity.

---

## 3. Verificação dos Dados

Após configurar o cliente, teste a conexão buscando dados do Sanity.io e exibindo-os em um componente React. Por exemplo:

```javascript
import React, { useEffect, useState } from 'react';
import client from './client';

const App = () => {
  const [data, setData] = useState([]);

  useEffect(() => {
    client
      .fetch('*[_type == "post"]')
      .then((data) => setData(data))
      .catch(console.error);
  }, []);

  return (
    <div>
      <h1>Posts</h1>
      <ul>
        {data.map((post) => (
          <li key={post._id}>{post.title}</li>
        ))}
      </ul>
    </div>
  );
};

export default App;
```

Certifique-se de ter um tipo de documento chamado `post` configurado no seu schema do Sanity para que este exemplo funcione corretamente.

---

## Observações

- Verifique a documentação oficial do Sanity.io para explorar mais funcionalidades.
- Configure corretamente o arquivo `.env` para armazenar informações sensíveis, como `projectId` e `dataset`, e atualize o `client.js` para usar essas variáveis de ambiente.

---

Com este passo a passo, sua aplicação React estará integrada ao Sanity.io com suporte para conteúdo dinâmico e renderização de blocos!


# Conectando-se ao Projeto Sanity
Após instalar o Sanity CLI e inicializar o seu projeto local, você pode se conectar ao seu projeto Sanity com o seguinte comando:

```bash
sanity login
```
Este comando autentica você no Sanity.io.

## 1. Criando um Novo Projeto (se necessário)
Se você ainda não tiver criado o projeto, pode fazer isso com:

```bash
sanity init
```

Durante o processo, ele perguntará se você deseja criar um novo projeto ou se conectar a um já existente. Ele também criará a pasta do Sanity no seu projeto.

## 2. Rodando o Studio Localmente
Para rodar a interface administrativa (Sanity Studio) localmente, use o comando:

```bash
sanity start
```

Isso iniciará o servidor local do Studio, onde você poderá gerenciar seu conteúdo.

## 3. Subindo o Projeto para a Nuvem
Quando você estiver pronto para enviar seu conteúdo para o Sanity na nuvem, use o comando:

```bash
sanity deploy
```
Esse comando irá publicar seu Studio local para a nuvem e criar um link público para o seu painel administrativo.

Observações
Verifique a documentação oficial do Sanity.io para explorar mais funcionalidades.
Configure corretamente o arquivo .env para armazenar informações sensíveis, como projectId e dataset, e atualize o client.js para usar essas variáveis de ambiente.