📌 openaiapp — Spring Boot + OpenAI ChatClient Example

This is a simple Spring Boot application demonstrating how to use Spring AI with OpenAI using the ChatClient API.
The app exposes a REST endpoint /ask where you can send a question and get an AI-generated response.

🚀 Features

✔ Spring Boot 3.5+

✔ Spring AI (OpenAI Starter)

✔ Secure API key loading using .env file

✔ Simple REST endpoint to query OpenAI

✔ Easy to extend (RAG, embeddings, Pinecone, etc.)

🛠️ Project Structure
openaiapp/
├── src/main/java/com/example/openaiapp/
│   ├── OpenaiappApplication.java
│   └── controller/
│       └── AiController.java
├── src/main/resources/
│   └── application.properties
├── .env
├── pom.xml
└── README.md

⚙️ 1. Requirements

Before running the project, ensure you have:

Java 17+

Maven

OpenAI API key

IntelliJ or VS Code (optional)

🔐 2. Setting Up Environment Variables

This project uses a .env file to securely load your API key instead of hardcoding it.

Create a file named:

.env


Add your OpenAI key:

SPRING_AI_OPENAI_API_KEY=your_api_key_here


⚠️ Make sure .env is ignored in .gitignore — this is already set in your project.

🔧 3. Configuration (application.properties)

Spring automatically reads env variables and maps them to Spring AI properties.

src/main/resources/application.properties:

spring.application.name=openaiapp
spring.ai.openai.api-key=${SPRING_AI_OPENAI_API_KEY}
spring.ai.openai.chat.options.model=gpt-4o-mini

🧠 4. Chat Endpoint

AiController.java:

@RestController
public class AiController {

    private final ChatClient chatClient;

    public AiController(ChatClient.Builder chatClientBuilder) {
        this.chatClient = chatClientBuilder.build();
    }

    @GetMapping("/ask")
    public String ask(@RequestParam String question) {
        return chatClient
                .prompt()
                .user(question)
                .call()
                .content();
    }
}

▶️ 5. Running the Project
Option 1: Using Maven
mvn spring-boot:run

Option 2: Using IntelliJ

Right-click OpenaiappApplication.java

Select Run

🌐 6. How to Use the API

Once the app is running at:

http://localhost:8080


Send a request:

http://localhost:8080/ask?question=What is Java?


Example output:

Java is a high-level, object-oriented programming language...

🧪 7. Example Curl Request
curl "http://localhost:8080/ask?question=Tell me a joke"

🛡️ 8. Security Notes

Never commit .env or API keys to GitHub.

.gitignore already includes .env.

Use environment variables in production (Docker, Kubernetes, etc.)

🤝 Contributing

Feel free to open issues or contribute new features—like adding Pinecone RAG or embeddings.

📄 License

This project is open-source and free to use.
