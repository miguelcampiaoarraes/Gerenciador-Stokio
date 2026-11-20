# Stokio — Sistema de Gestão Patrimonial e Agendamentos (FabLab SENAI)

<div align="center">

![Java](https://img.shields.io/badge/Java_17-0057FF?style=for-the-badge&logo=openjdk&logoColor=white)
![Spring Boot](https://img.shields.io/badge/Spring_Boot_3-161B22?style=for-the-badge&logo=springboot&logoColor=6DB33F)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-161B22?style=for-the-badge&logo=postgresql&logoColor=4169E1)
![Swagger/OpenAPI](https://img.shields.io/badge/OpenAPI_3-161B22?style=for-the-badge&logo=swagger&logoColor=85EA2D)
![Docker](https://img.shields.io/badge/Docker-161B22?style=for-the-badge&logo=docker&logoColor=2496ED)

**Projeto Integrador — Curso Técnico em Desenvolvimento de Sistemas (SENAI Petrópolis)**

</div>

---

## 📋 Visão Geral

O **Stokio** é uma solução completa desenvolvida para solucionar os desafios de controle de inventário, empréstimo de insumos técnicos e reservas de espaço no **FabLab do SENAI Petrópolis**. 

O sistema substitui planilhas descentralizadas por uma aplicação web robusta apoiada em **arquitetura em camadas (Spring Boot)** e persistência relacional **PostgreSQL**, oferecendo rastreabilidade de ponta a ponta de materiais, kits didáticos e equipamentos.

### Equipe de Desenvolvimento
- **Miguel Campião Arraes**
- Benício Guimarães
- Cauã França
- Gustavo Justen
- João Bernardo

---

## 🎯 Problema e Solução

| Cenário Anterior | Solução com o Stokio |
| :--- | :--- |
| Falta de visibilidade em tempo real dos itens disponíveis no laboratório. | Catálogo dinâmico de materiais e kits pedagógicos com controle de saldo de estoque. |
| Incerteza sobre a posse e devolução de equipamentos emprestados. | Módulo dedicado de rastreamento de empréstimos com registro de datas e usuários responsáveis. |
| Conflitos de horário no uso de bancadas e máquinas do laboratório. | Sistema de agendamento de espaços com aprovação e status configuráveis. |
| Dificuldade no registro de avarias ou manutenções. | Gestão de danos e histórico de manutenções vinculados a cada item ou kit. |

---

## ⚙️ Arquitetura e Tecnologias

O backend foi construído seguindo rigorosamente os padrões de mercado da engenharia de software Java:

- **Linguagem & Plataforma:** Java 17 LTS
- **Framework Principal:** Spring Boot 3
- **Camada Web & REST:** Spring Web MVC (`@RestController`, Content Negotiation JSON)
- **Persistência de Dados:** Spring Data JPA + Hibernate ORM
- **Bancos de Dados:** PostgreSQL (ambiente de execução/produção) e H2 Database (execução de testes em memória)
- **Documentação de API:** SpringDoc OpenAPI 3 / Swagger UI
- **Gerenciador de Dependências & Build:** Apache Maven com Maven Wrapper (`mvnw`)
- **Infraestrutura:** Docker (multi-stage build com Eclipse Temurin 17) e `render.yaml`

### Estrutura de Camadas (Package Structure)
```text
com.senai.pi.stokio
├── configs/         # Configurações globais (CORS, Swagger/OpenAPI, DataSeeder)
├── controllers/     # Controladores REST expondo os endpoints HTTP
├── models/          # Entidades de domínio JPA e regras de mapeamento ORM
├── repositories/    # Interfaces Spring Data JPA com operações de banco
├── services/        # Regras de negócio e validações da aplicação
└── Application.java # Ponto de entrada (Main Spring Boot Application)
```

---

## 📡 Principais Módulos da API REST

A aplicação expõe endpoints RESTful devidamente tipados e documentados via Swagger:

| Módulo | Entidade Principal | Operações Suportadas |
| :--- | :--- | :--- |
| **Materiais** | `Materiais`, `Categoria` | CRUD completo, controle de quantidade mínima, vínculo com categorias. |
| **Kits Pedagógicos** | `Kit`, `KitItem` | Montagem e composição de kits didáticos para aulas práticas e oficinas. |
| **Empréstimos** | `Emprestimo`, `EmprestimoKit` | Registro de saída, prazo de entrega, status de devolução e usuário associado. |
| **Agendamentos** | `Agendamento`, `AgendamentoLaboratorio` | Solicitação e reserva de horários para utilização do FabLab. |
| **Gestão de Danos** | `Danos` | Registro de avarias ocorridas durante aulas ou projetos para manutenção preventiva. |
| **Usuários** | `Usuario` | Cadastro de alunos, instrutores e coordenadores do laboratório. |

---

## 🚀 Como Executar o Projeto Localmente

### Pré-requisitos
- **Java Development Kit (JDK) 17** ou superior instalado.
- **Git** instalado.
- Banco de dados **PostgreSQL** instalado (opcional, o projeto possui perfil de fallback com H2).

### 1. Clonar o Repositório
```bash
git clone https://github.com/miguelcampiaoarraes/Gerenciador-Stokio.git
cd Gerenciador-Stokio
```

### 2. Configurar o Banco de Dados (PostgreSQL)
Verifique as propriedades no arquivo `src/main/resources/application.properties`:
```properties
spring.datasource.url=jdbc:postgresql://localhost:5432/stokio_db
spring.datasource.username=seu_usuario
spring.datasource.password=sua_senha
spring.jpa.hibernate.ddl-auto=update
```

### 3. Executar com o Maven Wrapper

#### No Windows (PowerShell / CMD):
```powershell
.\mvnw.cmd spring-boot:run
```

#### No Linux / macOS:
```bash
chmod +x ./mvnw
./mvnw spring-boot:run
```

### 4. Acessar a Documentação Interativa (Swagger)
Com a aplicação em execução, acesse pelo navegador:
```text
http://localhost:8080/swagger-ui.html
```

---

## 🧪 Execução de Testes Automatizados

O projeto conta com suite de testes com Spring Boot Starter Test e JUnit:
```powershell
.\mvnw.cmd test
```

---

## 🐳 Execução via Docker

Para rodar em ambiente isolado via contêiner:
```bash
# Construir a imagem Docker
docker build -t stokio-api .

# Executar o contêiner na porta 8080
docker run -p 8080:8080 stokio-api
```

---

<div align="center">
Desenvolvido no âmbito do SENAI Petrópolis • 2026
</div>
