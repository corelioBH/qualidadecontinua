 Os princípios fundamentais de qualidade de código são muito bem documentados e lidam com aspectos tais como:

* Tamanho de métodos
* Uso apropriado de comentários
* Nomes de variáveis
* Testes
* Lógica de programação
* Modularização

Uma referência sólida para esses conceitos é o excelente livro chamado Código Limpo, do Uncle Bob (Robert Martin), disponível [aqui](https://www.amazon.com.br/Código-limpo-Robert-C-Martin/dp/8576082675).

Existem diversas ferramentas e componentes no mercado que nos auxiliam a identificar  problemas de qualidade de código.Uma delas é o [SonarQube](https://www.sonarqube.org/), uma ferramenta grátis na versão Community e nas demais versões o preço varia de acordo com os recursos Developer/Enterprise/DataCenter.

Nesse tutorial, iremos criar um exemplo em .NET Core e avaliar a qualidade desse código com o SonarQube.

![img](https://cdn-images-1.medium.com/max/1600/1*RCowy6wN9oGxDOy7NRh8lQ.png)



Se você ainda não conhece o SonarQube, ele permite avaliar métricas de qualidade como Code Smells, Complexidade Ciclomática, Duplicação de Código, Cobertura de Testes, entre outras. Veja um exemplo abaixo.

![img](https://cdn-images-1.medium.com/max/1600/1*jVJuD5Prj9-_AI7kBBASYw.png)

Em nível de um sistema, ele permite também que você olhe cada mau cheito no seu código e te fornece racionais para que você atue e melhore o seu código.

![img](https://cdn-images-1.medium.com/max/1600/1*pJV2l4iixrKb8oeZCCQJ0g.png)



------

Vamos agora criar um ambiente e configurar o SonarQube com Docker + SonarQube  + Projeto .NET Core.

Vamos executar o compose para subir a imagem Sonarqube:

```
docker run -d --name sonarqube -p 9000:9000 sonarqube
```



Depois de alguns segundos, abra o seu navegador no endereço [http://localhost:9000](http://localhost:9000/)



![img](https://cdn-images-1.medium.com/max/1600/1*5afGvRU-qJ-iKfDkGLVkPg.png)

Enter the default credentials from the docker image

> **Login**: admin

> **Password**: admin

Será exibida uma interface para inserir informações sobre o projeto:



![img](https://cdn-images-1.medium.com/max/1600/1*LSwQLwopN4eT8oo_z6VHbg.png)

Após clicar em Generate será exibida a seguinte tela:

![img](https://cdn-images-1.medium.com/max/1600/1*_7E_uxPCZKM5bTfy7nwC1w.png)

Nesse momento selecione a linguagem do seu projeto e insira uma key que será usada como Token:

![img](https://cdn-images-1.medium.com/max/1600/1*zpXA7rCPHHdRU1tYMrb7lQ.png)

Após clicar em Done, as seguintes informações serão exibidas:

![img](https://cdn-images-1.medium.com/max/1600/1*DWQj6cOFxU1LSGDJB5KFOw.png)

Anote a key marcada na imagem acima e clique em Finish this tutorial no canto inferior direito.

Feito isso seu projeto está criado e seu ambiente está pronto para realizar a primeira análise:

![img](https://cdn-images-1.medium.com/max/1600/1*sdD_-XYhOhJVzX333zZQtg.png)

Abra novamente o CMD e crie uma nova solution e projeto, altere o nome da solution e projeto para o nome gerado pelo comando new sln / console.

```
dotnet new sln
dotnet new console
dotnet sln awesomeproject.sln add awesomeproject.csproj
```



![img](https://cdn-images-1.medium.com/max/1600/1*v0mYUIj5eIMWzsEKDdi3ew.png)

Agora vamos para a parte do SonarQube, para o .NET Core temos uma tool nativa, para instalar execute o seguinte comando:

```sh
dotnet tool install --global dotnet-sonarscanner
```

```
dotnet sonarscanner begin /d:sonar.login=admin /d:sonar.password=bitnami /k:”AwesomeKey”
```

O Login pode ser substituído pela Key gerada acima, ficando apenas:

```
dotnet sonarscanner begin /d:sonar.login=keygerada /k:”AwesomeKey”
```

![img](https://cdn-images-1.medium.com/max/1600/1*OXUhCU_AbDVHWL2wjN0G6Q.png)

Agora vamos executar um build do projeto:

```
dotnet build
```

![img](https://cdn-images-1.medium.com/max/1600/1*l7MZN68KmVLTBssmTxpKjw.png)

dotnet build

E para finalizar o processo, vamos executar o comando para encerrar a análise:

```
dotnet sonarscanner end /d:sonar.login=admin /d:sonar.password=bitnami
```

Ou

```
dotnet sonarscanner end /d:sonar.login=keygerada
```

![img](https://cdn-images-1.medium.com/max/1600/1*lt7QDn7-qQ0n0OBkpB4CDA.png)

Process done

Finalizado o processo, podemos voltar para o dashboard (http://localhost:9000) e teremos algumas informações:



![img](https://cdn-images-1.medium.com/max/1600/1*wdZQd41FBGI80i_U7i_YYw.png)



![img](https://cdn-images-1.medium.com/max/1600/1*iaVWil7-w9IDjDRAP0sosQ.png)

---

## Execução em um projeto real

Agora é com você. Escolha um projeto complexo em .NET Core (que você tenha construído ou da Internet) e gere o mesmo processo de análise para ele. Busque identificar as lacunas técnicas do seu projeto e o que você faria para ajustá-las. Faça um ajuste em um dívida técnica e repita o processo.

---

## Análise de Projetos Reais

Abra o portal SonarCloud (https://sonarcloud.io/about). Ele mantém um repositório de projetos com análise em diversas linguagens.

Você pode olhar um repositório de exemplos aqui:

https://sonarcloud.io/explore/projects?sort=-analysis_date

A sua missão é analisar um projeto de exemplo em JS. .NET disponibilizado aqui: https://sonarcloud.io/dashboard?id=partsunlimited.johnzheng

Avalie como esse projeto está atendendo aos seguintes critérios técnicos. Justifique sua resposta:

* Segurança
* Cobertura de testes
* Duplicação de código
* Confiabilidade
* Complexidade ciclomática

Assuma agora que você é responsável pela redução do débito técnico de manutenibilidade? Que ações você faria, em termos práticos. Por quê? 
