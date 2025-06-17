# Executando um servidor Java com Spring Boot

---

## ✅ Passo a Passo: Subir somente um servidor em Java com Spring Boot

### 1. **Criar o projeto no Spring Initializr**

Acesse: [https://start.spring.io](https://start.spring.io)

Preencha assim:

-   **Project**: Maven ou Gradle (escolha o que preferir)
-   **Language**: Java
-   **Spring Boot**: escolha a versão estável mais recente
-   **Project Metadata**:

    -   Group: `com.exemplo`
    -   Artifact: `meuservidor`
    -   Name: `meuservidor`
    -   Package name: `com.exemplo.meuservidor`

-   **Dependencies** (adicione conforme a necessidade):

    -   `Spring Web` (essencial para servidor REST)
    -   `Spring Boot DevTools` (opcional, para desenvolvimento)

Clique em **Generate**, o que vai baixar um `.zip`.

---

### 2. **Importar o projeto na sua IDE (IntelliJ, VS Code, Eclipse)**

-   Descompacte o `.zip`
-   Abra o projeto na sua IDE
-   O arquivo principal estará em:

```
src/main/java/com/exemplo/meuservidor/MeuservidorApplication.java
```

---

### 3. **Arquivo main**

Esse arquivo já contém a estrutura básica para subir o servidor:

```java
// Define o pacote onde esta classe está localizada.
// Isso é importante para organização do projeto e para o Spring saber onde procurar os componentes.
package com.example.meuservidor;

// Importa a classe responsável por iniciar a aplicação Spring Boot.
import org.springframework.boot.SpringApplication;

// Importa a anotação que configura a aplicação como uma aplicação Spring Boot,
// ativando autoconfiguração, escaneamento de componentes e outras funcionalidades.
import org.springframework.boot.autoconfigure.SpringBootApplication;

// Marca esta classe como a classe principal da aplicação Spring Boot.
// Essa anotação é um atalho para @Configuration, @EnableAutoConfiguration e @ComponentScan.
@SpringBootApplication
public class MeuservidorApplication {

	// Método principal que inicia a aplicação Java.
	public static void main(String[] args) {
		// Esse método executa a aplicação Spring Boot,
		// inicializa o contexto da aplicação e o servidor embutido (por padrão, Tomcat).
		SpringApplication.run(MeuservidorApplication.class, args);
	}

}

```

O servidor servidor Spring Boot está corretamente, mas \*\*não encontrará rota ou recurso para responder à URL (por exemplo, `http://localhost:8080/`).

---

Não existe rota mapeada para o caminho, teremos que criar.

## ✅ Como resolver e exibir algo no navegador

Você precisa criar **um controller com uma rota mapeada**. Exemplo mínimo:

### 1. Crie uma nova classe em `src/main/java/com/exemplo/meuservidor/HelloController.java`

Dentro da pasta meuservidor crie o arquivo : HelloController.java

```java
// Define o pacote onde esta classe está localizada.
// Isso ajuda o Spring Boot a localizar e registrar os componentes automaticamente.
package com.example.meuservidor;

// Importa a anotação @GetMapping, que é usada para mapear requisições HTTP GET para métodos específicos.
import org.springframework.web.bind.annotation.GetMapping;

// Importa a anotação @RestController, que combina @Controller e @ResponseBody,
// indicando que os métodos retornam dados diretamente no corpo da resposta (geralmente JSON ou texto simples).
import org.springframework.web.bind.annotation.RestController;

// Define a classe como um controlador REST.
// Isso faz com que o Spring reconheça esta classe como um componente web que lida com requisições HTTP.
@RestController
public class HelloController {

    // Mapeia o caminho "/" (raiz do site) para este método.
    // Quando alguém acessar http://localhost:8080/ com método GET, este método será executado.
    @GetMapping("/")
    public String hello() {
        // Retorna uma mensagem simples de texto como resposta da requisição.
        return "Servidor Spring Boot rodando com sucesso!";
    }

}

```

A classe é sinalizada como @RestController, o que significa que está pronta para ser usada pelo Spring MVC para lidar com solicitações web. @GetMappingmapeia /para o index()método. Quando invocado em um navegador ou usando curl na linha de comando, o método retorna texto puro. Isso ocorre porque @RestControllercombina @Controllere @ResponseBody, duas anotações que resultam em solicitações web retornando dados em vez de uma visualização.

Construindo uma aplicação com Spring Boot:
https://spring.io/guides/gs/spring-boot

---

### 2. Rode novamente a aplicação

#### ▶️ Via IDE (mais fácil)

-   Clique com o botão direito no método `main` → **Run 'MeuservidorApplication.main()'**

#### 🧪 Via terminal

Acesse a pasta do projeto e use:

Se já estiver rodando, **salve e espere reiniciar automaticamente** (se estiver com DevTools) ou pare e rode de novo com:

```bash
./mvnw spring-boot:run
```

ou (caso já tenha gerado o `.jar`):

```bash
java -jar target/meuservidor-0.0.1-SNAPSHOT.jar
```

### 3. Acesse no navegador:

```
http://localhost:8080/
```

Agora você verá:

```
Servidor Spring Boot rodando com sucesso!
```

# Instalação:

Para rodar **Java no VS Code** com suporte completo (compilar, executar e usar frameworks como Spring Boot), você precisa instalar os seguintes requisitos básicos:

---

## ✅ 1. **Java JDK (Java Development Kit)**

-   **Versão recomendada:** JDK 17 ou superior (ex: JDK 21).
-   Instala o compilador `javac` e a JVM (`java`).

🔗 Download oficial (OpenJDK):
[https://adoptium.net/pt-br/temurin/](https://adoptium.net/pt-br/temurin/)

> Após instalar, confirme no terminal:

```bash
java -version
javac -version
```

---

## ✅ 2. **Visual Studio Code**

-   Baixe o VS Code em:
    [https://code.visualstudio.com/](https://code.visualstudio.com/)

---

## ✅ 3. **Extensão Java para VS Code**

Instale as extensões via a aba **Extensions** (`Ctrl+Shift+X`), procure e instale:

-   🔹 **Extension Pack for Java** (recomendado)

    -   Inclui:

        -   Language Support for Java™ (by Red Hat)
        -   Debugger for Java
        -   Java Test Runner
        -   Maven for Java
        -   Java Dependency Viewer

Ou instale separadamente:

-   `Language Support for Java(TM) by Red Hat`
-   `Debugger for Java`
-   `Java Test Runner`

---

## ✅ 4. (Opcional) **Maven ou Gradle**

Para projetos maiores ou como o Spring Boot.

-   **Maven:**
    [https://maven.apache.org/download.cgi](https://maven.apache.org/download.cgi)
    Depois, verifique:

    ```bash
    mvn -v
    ```

-   **Gradle:**
    [https://gradle.org/install/](https://gradle.org/install/)

---

## ✅ 5. (Opcional) **Spring Boot Tools**

Se você for trabalhar com Spring:

-   Instale a extensão:
    🔹 `Spring Boot Extension Pack`

---

## ✅ Exemplo de Teste

Crie um arquivo `Hello.java`:

```java
public class Hello {
    public static void main(String[] args) {
        System.out.println("Olá, Java no VS Code!");
    }
}
```

Execute com:

```bash
javac Hello.java
java Hello
```

---

Se quiser, posso montar um passo a passo visual com prints para alunos também. Deseja?
