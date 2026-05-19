# Guia de Adaptacao de Agentes e Comandos (Multi-stack)

Este repositório e um **soft-skill reutilizavel** para diferentes projetos.
A ideia e usar a mesma estrutura-base de agentes e comandos, adaptando o conteudo para a tecnologia do projeto alvo.

## Objetivo

Padronizar a forma de trabalhar com agentes em projetos diferentes, sem criar novas skills, apenas ajustando instrucoes.

Estrutura usada neste repositório:

```text
.claude/
  agents/
    code-reviewer.md
    commit-message-generator.md
    engenheiro-react-senior.md
    qa-test-documentation-generator.md
    revisor-de-codigo.md
  commands/
    executar-task-react.md
```

## Estrutura recomendada no projeto alvo

No projeto que vai consumir este soft-skill, mantenha:

```text
.claude/
  agents/
  commands/
```

Se a API for FastAPI (Python), por exemplo, você pode criar comandos como:

- `executar-task-python.md`
- `novo-endpoint.md`
- `run-tests.md`
- `migration.md`

## Como adaptar (passo a passo)

1. Levante o contexto tecnico do projeto
- Linguagem principal
- Framework
- Gerenciador de dependencias
- Ferramenta de teste
- Estrutura de pastas
- Regras de qualidade (lint, formatacao, arquitetura)

2. Extraia as regras de engenharia do projeto
- Use `.cursor/rules` (quando existir)
- Use `README`, `CONTRIBUTING`, `requirements.txt`, `pyproject.toml`, `pom.xml`, `.csproj`, `package.json`, etc.
- Transforme essas regras em instrucoes explicitas dentro dos agentes

3. Adapte os agentes por responsabilidade (nao por framework)
- `code-reviewer`: revisao de qualidade e conformidade
- `revisor-de-codigo`: revisao + aplicacao de correcoes
- `qa-test-documentation-generator`: documentacao para QA e plano de testes
- `commit-message-generator`: mensagens de commit padronizadas
- Agente especializado (ex.: React, FastAPI, Spring, .NET, Angular)

4. Adapte os comandos por fluxo de trabalho
- Cada comando deve orquestrar a ordem dos agentes
- Exemplo de fluxo: implementar -> revisar -> corrigir criticos -> documentar QA -> gerar commit

5. Valide o fluxo na pratica
- Rode o comando em uma tarefa real
- Verifique se os agentes respeitam as regras do projeto
- Ajuste prompts ate eliminar ambiguidades

## Checklist de adaptacao

- [ ] Agentes com `name`, `description` e instrucoes claras
- [ ] Comandos chamando agentes na ordem correta
- [ ] Regras do projeto refletidas nos agentes
- [ ] Tecnologias e ferramentas reais do projeto mapeadas
- [ ] Padrao de review e testes definido
- [ ] Padrao de commits definido (Conventional Commits)

## Padrao de arquivo de agente

Use este template como base:

```md
---
name: nome-do-agente
description: Quando usar este agente e exemplos de acionamento
model: sonnet
color: blue
---

Voce e um especialista em [dominio].

Responsabilidades:
1. ...
2. ...

Regras obrigatorias do projeto:
- Seguir .cursor/rules
- Seguir convencoes de pasta e nomenclatura
- Seguir stack e bibliotecas oficiais do projeto

Formato de saida:
- Secao 1
- Secao 2
- Secao 3
```

## Padrao de arquivo de comando

Use este template como base:

```md
Use o @agente-especialista para executar a tarefa.

Depois, SEMPRE chame o @code-reviewer para revisar o resultado.

Depois, SEMPRE chame o @agente-especialista para aplicar SOMENTE mudancas criticas.

Depois, SEMPRE chame o @qa-test-documentation-generator.

Por fim, SEMPRE chame o @commit-message-generator.
```

## Adaptacao por tecnologia

### Python + FastAPI (foco principal)

Como adaptar agentes:
- Revisao deve checar `requirements.txt` ou `pyproject.toml`
- Validar padrao FastAPI (routers, schemas, dependency injection, status codes)
- Garantir tratamento de excecoes e validacao com Pydantic
- Cobrar testes com `pytest` e testes de endpoint

Como adaptar comandos:
- Criar comando para novo endpoint FastAPI
- Criar comando para migrations (Alembic, se aplicavel)
- Criar comando para rodar testes e lint

Exemplo de orientacoes para agente FastAPI:
- Verifique separacao entre camada de rota, servico e repositorio
- Nao misture regra de negocio no router
- Garanta tipagem e contratos de request/response
- Documente impacto para QA

### Java (Spring Boot)

Como adaptar agentes:
- Considerar `pom.xml` ou `build.gradle`
- Revisar controllers, services, repositories, DTOs
- Validar tratamento global de excecoes
- Cobrar testes unitarios e de integracao

Como adaptar comandos:
- Comando para novo endpoint REST
- Comando para revisao + ajustes de qualidade
- Comando para executar testes (`mvn test` ou `gradle test`)

### C# / .NET Core

Como adaptar agentes:
- Considerar `.csproj`, `Program.cs`, `appsettings`
- Revisar Controllers/Minimal APIs, Services, Repositories
- Validar injecao de dependencia e middlewares
- Cobrar testes com xUnit/NUnit

Como adaptar comandos:
- Comando para criar endpoint
- Comando para rodar testes (`dotnet test`)
- Comando para revisao e correcao automatica

### Angular

Como adaptar agentes:
- Considerar `angular.json`, `package.json`, estrutura `src/app`
- Revisar componentes, servicos, guards, interceptors
- Validar padrao RxJS e gerenciamento de estado
- Cobrar testes com Karma/Jasmine ou Jest

Como adaptar comandos:
- Comando para implementar feature de tela
- Comando para revisao de qualidade frontend
- Comando para testes (`ng test`) e lint

## Exemplo pratico para API FastAPI

Supondo uma API Python/FastAPI com `requirements.txt` e estrutura de modulos definida:

1. Copie os agentes base para `.claude/agents`
2. Crie um agente especializado, por exemplo `fastapi-endpoint.md`
3. Crie comandos em `.claude/commands`, por exemplo:
- `novo-endpoint.md`
- `review.md`
- `run-tests.md`
4. Nos textos dos agentes/comandos, substitua referencias React por FastAPI
5. Inclua as regras reais da API (arquitetura, testes, migrations, seguranca)

## Regras importantes para manter consistencia

- Nao criar skills novas para este objetivo
- Priorizar instrucoes claras, objetivas e acionaveis
- Evitar regras vagas como "faca o melhor"
- Sempre explicitar criterio de qualidade e criterio de aceite
- Sempre fechar o fluxo com documentacao QA e mensagem de commit

## Resultado esperado

Ao final da adaptacao, o projeto deve ter:

- Agentes reutilizaveis e aderentes ao stack
- Comandos que orquestram fluxo fim a fim
- Revisao tecnica padronizada
- Documentacao de QA consistente
- Mensagens de commit padronizadas

---

## Proximos passos

Veja o arquivo [PROMPT_PRATICO.md](PROMPT_PRATICO.md) para prompts prontos que voce pode copiar e colar para solicitar a adaptacao ao seu assistente de codigo (Claude, Copilot, etc.).

Ha prompts específicos para:
- Python + FastAPI (foco principal)
- Java + Spring Boot
- C# + .NET Core
- Angular
