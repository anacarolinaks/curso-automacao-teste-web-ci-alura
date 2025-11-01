# Curso: Cypress — Automação de Testes Web e CI

Este repositório contém o material e os exemplos práticos do curso "Cypress: automatização de testes web e CI". O objetivo do curso e deste projeto é ensinar como:

- Automatizar testes end-to-end (E2E) com Cypress.
- Integrar testes em pipelines de Integração Contínua (CI) com GitHub Actions.
- Integrar com Cypress Cloud para colaboração e visualização de runs.
- Enriquecer cenários usando faker.js e plugins do Cypress.
- Usar técnicas de Inteligência Artificial para melhorar escrita e eficiência dos testes.
- Aplicar boas práticas para aumentar produtividade em testes automatizados.

## Conteúdo do repositório

- `cypress/` — testes E2E, fixtures e suporte.
- `server/` e `src/` — exemplos de backend e API usados nos testes (quando aplicável).
- `.github/workflows/cypress.yml` — pipeline de CI (GitHub Actions) para rodar os testes.
- `package.json` — scripts e dependências do projeto.

## Pré-requisitos

- Node.js 18+ e npm ou yarn
- Git
- Conta no Cypress Cloud (opcional, recomendado para integração)

No Windows PowerShell, recomenda-se abrir o terminal na raiz do projeto:

```powershell
cd "C:\Users\kojim\OneDrive\Área de Trabalho\Cursos\curso-automacao-teste-web-ci-alura"
```

## Instalação

Instale as dependências com npm (ou yarn):

```powershell
npm install
# ou
npm ci
```

Observação: o `package.json` do repositório já contém dependências principais como `cypress`, `cypress-plugin-api` e `mochawesome`.

## Scripts úteis

Os scripts definidos em `package.json` incluem:

- `npm run lint` — executa o ESLint nos arquivos do Cypress.
- `npm run lint:fix` — executa o ESLint e tenta corrigir problemas automaticamente.
- `npm run test:browser:edge` — executa os testes no navegador Edge.
- `npm run test:tablet` — executa os testes com viewport configurado para tablet.

Para rodar uma execução padrão do Cypress em modo headless:

```powershell
npx cypress run
```

Para abrir o Cypress Test Runner em modo interativo (útil durante desenvolvimento):

```powershell
npx cypress open
```

## Relatórios

O projeto usa `mochawesome` para geração de relatórios. Verifique a pasta `cypress/results` (ou `results/`) para arquivos HTML gerados por execuções anteriores.

## Integração contínua (GitHub Actions)

Este repositório já contém um workflow de exemplo em `.github/workflows/cypress.yml` que:

- Instala dependências
- Executa os testes com Cypress
- Publica relatórios (configurado conforme o workflow do curso)

Dicas para CI:

- Cache de dependências (npm) para reduzir tempo de build.
- Configurar matrices de navegador se quiser rodar em múltiplos browsers.
- Exportar artefatos (relatórios, vídeos, screenshots) para inspecionar falhas.

## Integração com Cypress Cloud

Para integrar com o Cypress Cloud (anteriormente Cypress Dashboard):

1. Crie/entre na sua conta do Cypress Cloud.
2. Obtenha o `record key` do seu projeto no Cloud.
3. No GitHub, adicione o segredo `CYPRESS_RECORD_KEY` no repositório (Settings > Secrets).
4. No workflow do GitHub Actions, adicione a flag `--record --key ${{ secrets.CYPRESS_RECORD_KEY }}` no comando de execução do cypress, por exemplo:

```yaml
- name: Run Cypress
  run: npx cypress run --record --key ${{ secrets.CYPRESS_RECORD_KEY }}
```

Isso permitirá visualizar runs, vídeos e screenshots no painel do Cypress Cloud e facilitar a colaboração.

## Faker.js e plugins para dados realísticos

Usar dados realísticos aumenta a robustez dos testes. No repositório há exemplos de fixtures em `cypress/fixtures/`.

Exemplo rápido de uso do `faker` em um teste (instale `@faker-js/faker` ou `faker`):

```javascript
// cypress/e2e/exemplo-faker.cy.js
import { faker } from '@faker-js/faker'

describe('Exemplo com faker', () => {
  it('preenche formulário com dados falsos', () => {
    const nome = faker.person.fullName()
    const email = faker.internet.email()

    cy.visit('/cadastro')
    cy.get('#nome').type(nome)
    cy.get('#email').type(email)
    cy.get('form').submit()
    cy.contains('Cadastro realizado com sucesso')
  })
})
```

Plugins úteis do ecossistema Cypress:

- `cypress-plugin-api` — facilitar chamadas API dentro de testes (já presente nas dependências).
- `cypress-localstorage-commands` — manipular localStorage entre testes.
- `cypress-file-upload` — upload de arquivos em testes.

Instale um plugin com:

```powershell
npm install -D @faker-js/faker cypress-localstorage-commands cypress-file-upload
```

E registre-os em `cypress/support/commands.js` quando necessário.

## Uso de Inteligência Artificial (IA)

IA pode acelerar a escrita e manutenção de testes. Aqui estão usos práticos e seguros:

- Gerar templates de teste e exemplos a partir de descrições (use prompts que descrevam o fluxo).
- Refatorar seletores frágeis sugerindo seletores mais robustos (data-* attributes).
- Gerar dados de teste com estratégias inteligentes (combinar faker com regras de negócio).
- Sugerir cenários adicionais de teste com base em cobertura atual.

Exemplo de prompt simples para IA (ajuste conforme sua ferramenta):

"Escreva um teste E2E com Cypress que preencha o formulário de cadastro com campos: nome, email, senha — usando seletores com data-testid — e verifique a mensagem de sucesso."

Observações de segurança:

- Não envie dados sensíveis para serviços de IA sem antes anonimizar e obter consentimento.
- Valide as sugestões geradas pelo modelo; não execute código sem revisão.

## Boas práticas e produtividade

- Preferir seletores estáveis: use atributos `data-testid` ou `data-cy` ao invés de classes ou textos dinâmicos.
- Isolar comportamentos em comandos customizados (`cypress/support/commands.js`).
- Usar fixtures e factories para criar dados previsíveis em testes.
- Evitar dependência entre testes — cada teste deve ser independente.
- Executar testes em paralelo no CI e dividir por pastas/suites para reduzir tempo total.
- Registrar screenshots, vídeos e gravações de rede para depuração.

## Estrutura sugerida de arquivos e exemplos

- `cypress/e2e/` — arquivos `.cy.js` com os testes.
- `cypress/fixtures/` — JSONs com dados fictícios.
- `cypress/support/` — comandos customizados e configuração global.
- `cypress.config.js` — configuração do Cypress (timeouts, baseUrl, env).

## Exemplos de execução no PowerShell

Instalar dependências:

```powershell
npm install
```

Apenas lint:

```powershell
npm run lint
```

Executar testes no Edge (script disponível):

```powershell
npm run test:browser:edge
```

Executar testes com viewport de tablet (script disponível):

```powershell
npm run test:tablet
```

Abrir runner interativo:

```powershell
npx cypress open
```

Executar em modo headless e gerar relatório mochawesome (exemplo):

```powershell
npx cypress run --reporter mochawesome
```

## Próximos passos e sugestões

- Adicionar badges no README para: build CI, cobertura de testes e status do Cypress Cloud.
- Configurar execução paralela no CI e gravar artefatos por job.
- Adicionar exemplos de testes usando TypeScript (se desejar migrar `/src` e `/cypress` para TS).
- Criar um pequeno conjunto de testes de integração com API usando `cypress-plugin-api`.
- Adicionar exemplos de prompts e snippets de IA em uma pasta `docs/ia/` para facilitar reutilização.

## Contribuição

Contribuições são bem-vindas. Abra issues e PRs com mudanças ou melhorias nos testes e no pipeline.

---

Documentação gerada automaticamente com base no conteúdo do repositório e no escopo do curso.
