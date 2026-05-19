# Prompts Práticos para Adaptação de Agentes e Comandos

Use os prompts abaixo como base para solicitar ao Claude/Copilot a adaptação da estrutura de agentes e comandos para seu projeto.

---

## Prompt Genérico (Use como base, adapte conforme necessário)

```
Você tem uma estrutura de soft-skill com agentes e comandos reutilizáveis em:

/meu-projeto/.claude/agents
/meu-projeto/.claude/commands

Preciso adaptar essa estrutura para meu projeto [TIPO_PROJETO] em [TECNOLOGIA].

Detalhes do meu projeto:
- Stack: [STACK_ESPECÍFICA]
- Estrutura de pastas: [ESTRUTURA]
- Ferramenta de teste: [TESTE]
- Linter/Formatador: [LINT]
- Arquivo de dependências: [DEPS_FILE]
- Requisitos de qualidade: [REGRAS_ESPECIAIS]

Por favor:
1. Copie os agentes base e adapte-os para [TECNOLOGIA]
2. Revise as responsabilidades e regras para refletir a realidade do projeto
3. Crie comandos específicos para [TECNOLOGIA] que orquestrem o fluxo de trabalho
4. Certifique-se que cada agente entende as convenções e padrões do projeto
5. NÃO crie skills novas, apenas adapte as instruções existentes

Resultado esperado: estrutura pronta em .claude/agents e .claude/commands
```

---

## Exemplos Específicos por Tecnologia

### Python + FastAPI

```
Crie a estrutura dos agentes com base no exemplo em:

/meu-projeto/.claude/agents
/meu-projeto/.claude/commands

Lembrando que esta é uma API em Python com FastAPI.

Características do projeto:
- requirements.txt com FastAPI, Pydantic, SQLAlchemy, Alembic
- Estrutura: app/routers/, app/schemas/, app/models/, app/services/, app/repositories/
- Testes com pytest
- Linter: flake8 e black
- Migrations com Alembic

Adapte os agentes e crie comandos específicos para:
1. Criar novo endpoint FastAPI
2. Revisar código com lint/formatação
3. Rodar testes e migrations
4. Gerar mensagens de commit

Estrutura desejada em .claude/:
- agents/ com agentes base + especializado FastAPI
- commands/ com executar-task-python.md, novo-endpoint.md, review.md, run-tests.md

NÃO crie skills, apenas adapte instruções.
```

### Java + Spring Boot

```
Crie a estrutura dos agentes com base no exemplo em:

/meu-projeto/.claude/agents
/meu-projeto/.claude/commands

Lembrando que este é um projeto Java com Spring Boot.

Características do projeto:
- pom.xml com Spring Boot, Spring Data, Spring Security
- Estrutura: src/main/java/com/app/controller/, service/, repository/, entity/, dto/
- Testes com JUnit e MockMVC
- Formatador: Google Java Format
- Linter: SonarQube rules ou Checkstyle

Adapte os agentes e crie comandos específicos para:
1. Criar novo endpoint REST com Spring
2. Revisar código com padrões Spring
3. Rodar testes unitários e integração
4. Gerar mensagens de commit com Conventional Commits

Estrutura desejada em .claude/:
- agents/ com agentes base + especializado Spring Boot
- commands/ com executar-task-java.md, novo-endpoint.md, review.md, run-tests.md

NÃO crie skills, apenas adapte instruções.
```

### C# + .NET Core

```
Crie a estrutura dos agentes com base no exemplo em:

/meu-projeto/.claude/agents
/meu-projeto/.claude/commands

Lembrando que este é um projeto C# com .NET Core.

Características do projeto:
- .csproj com dependências NuGet
- Estrutura: Controllers/, Services/, Repositories/, Models/, DTOs/
- Program.cs com Dependency Injection
- Testes com xUnit ou NUnit
- Formatador: Roslyn analyzers
- Linter: StyleCop rules

Adapte os agentes e crie comandos específicos para:
1. Criar novo endpoint com Minimal APIs ou Controllers
2. Revisar código com padrões .NET Core
3. Executar testes unitários e integração (dotnet test)
4. Gerar mensagens de commit com Conventional Commits

Estrutura desejada em .claude/:
- agents/ com agentes base + especializado .NET Core
- commands/ com executar-task-csharp.md, novo-endpoint.md, review.md, run-tests.md

NÃO crie skills, apenas adapte instruções.
```

### Angular

```
Crie a estrutura dos agentes com base no exemplo em:

/meu-projeto/.claude/agents
/meu-projeto/.claude/commands

Lembrando que este é um projeto Angular.

Características do projeto:
- angular.json e package.json
- Estrutura: src/app/components/, services/, guards/, interceptors/, models/
- TypeScript com tipos estritamente tipados
- Testes com Karma/Jasmine ou Jest
- Formatador: Prettier
- Linter: ESLint com regras Angular

Adapte os agentes e crie comandos específicos para:
1. Implementar novo componente ou feature Angular
2. Revisar código com padrões Angular e RxJS
3. Executar testes (ng test) e lint (ng lint)
4. Gerar mensagens de commit com Conventional Commits

Estrutura desejada em .claude/:
- agents/ com agentes base + especializado Angular
- commands/ com executar-task-angular.md, nova-feature.md, review.md, run-tests.md

NÃO crie skills, apenas adapte instruções.
```

---

## Checklist de Validação Após Adaptação

Depois de adaptar, valide:

- [ ] Todos os agentes têm `name`, `description` em YAML frontmatter
- [ ] Cada agente referencia as regras reais do projeto (arquivos específicos, convenções)
- [ ] Comandos chamam agentes na ordem correta (especialista → code-reviewer → corrigir → qa-doc → commit)
- [ ] Exemplos de uso são específicos para a tecnologia do projeto
- [ ] Nenhum agente faz suposições sobre código, arquitetura ou padrões não reais
- [ ] Cada comando termina com mensagem de commit documentada

---

## Exemplo de Fluxo Completo

### Passo 1: Preparar contexto
```bash
cd meu-projeto/
# Tenha à mão:
# - requirements.txt (ou pyproject.toml, pom.xml, .csproj, package.json)
# - README ou CONTRIBUTING com regras do projeto
# - Estrutura de pastas do projeto
# - Arquivo de linting/formatação (flake8, eslint, etc.)
```

### Passo 2: Copiar estrutura base
```bash
cp -r ~/meu-projeto/.claude/agents .
cp -r ~/meu-projeto/.claude/commands .
```

### Passo 3: Usar o prompt de adaptação
Cole um dos prompts específicos acima no seu assistente de código (Claude/Copilot) e siga as instrucoes retornadas.

### Passo 4: Validar
- Rode um comando em uma tarefa real
- Verifique se as regras do projeto estão sendo respeitadas
- Ajuste prompts até eliminar ambiguidades

---

## Dúvidas Frequentes

**P: Preciso criar skills novas?**
R: Não. A ideia é adaptar os agentes e comandos já existentes. Skills são extras para casos muito específicos.

**P: Posso reutilizar alguns agentes como estão?**
R: Sim! `commit-message-generator` e `qa-test-documentation-generator` são agnósticos de tecnologia. Adapte apenas os especializados e os comandos.

**P: E se meu projeto usa múltiplas tecnologias?**
R: Crie múltiplos comandos. Ex: `executar-task-python.md`, `executar-task-frontend.md`. Cada um orquestra agentes apropriados.

**P: Como garantir que os agentes respeitam as regras?**
R: Sempre copie os arquivos `.cursor/rules` para o projeto e referencie-os nos agentes. Isso garante que as regras são sempre consultadas.

---

## Próximos Passos

1. Escolha a tecnologia do seu projeto
2. Use o prompt específico acima
3. Valide a estrutura gerada
4. Documente desvios ou customizações no seu projeto


## Exemplo prompt:
Crie a estrutura dos agentes com base no exemplo em anexo, lembrando que essa e uma api em pyhon com fastapi, em anexo o requirements do projeto e a estrutura da api.

no AGENTS.md deixe claro que existem 2 projetos: frontend e backend. Inclua os comandos para instalar dependências, rodar o projeto, também as portas onde cada um deles roda. Além disso, crie
um ponteiro para cada rule e skill existente, elas estão na pasta agents/rules e agents/skills