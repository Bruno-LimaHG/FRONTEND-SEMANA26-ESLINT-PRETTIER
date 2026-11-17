# Roteiro de Atividade Prática — Resolução Completa

**Componente Curricular:** Desenvolvimento Front-End  
**Título da Atividade:** Configurando ESLint e Prettier para padronização de código  
**Documento de Origem:** `[SIS]ANO2C3B4S26A3AP.docx`  
**Semana:** 26  

---

## 👤 Identificação do Aluno e Disciplina
- **Nome do Aluno:** Bruno De Lima
- **Turma:** 3° B
- **Professor:** Pedro Yokada
- **Matéria:** Front-End
- **Data de Resolução:** 17/11/2026

---

## 1. Contextualização e Cenário da Atividade

No desenvolvimento moderno de aplicações Front-End em equipe, a consistência, a legibilidade e a qualidade do código são cruciais para evitar débitos técnicos, facilitar a manutenção e prevenir bugs em produção. Em times onde cada desenvolvedor adota preferências individuais de escrita (como uso ou omissão de ponto e vírgula, aspas simples vs. duplas, indentação com tabs ou espaços), o histórico de commits no Git torna-se poluído com alterações cosméticas irrelevantes.

Para sanar esse problema e automatizar o controle de qualidade, configuramos e integramos duas ferramentas essenciais do ecossistema JavaScript:
1. **ESLint:** Ferramenta de **análise estática (linter)** que examina o código-fonte em busca de falhas sintáticas, padrões inconsistentes, variáveis declaradas e não utilizadas e possíveis bugs lógicos.
2. **Prettier:** Ferramenta opinativa de **formatação automática de código (code formatter)**, que garante estilo visual estrito e uniforme em todo o projeto.

---

## 2. Etapas de Configuração do Ambiente e Dependências

### 2.1 Inicialização do Projeto Node.js
No terminal (PowerShell / Bash), cria-se o diretório do projeto e inicializa-se o gerenciador de pacotes com as configurações padrão:

```bash
# 1. Criação do diretório do projeto
mkdir eslint-prettier-project
cd eslint-prettier-project

# 2. Inicialização do package.json com valores default
npm init -y
```

### 2.2 Instalação das Ferramentas como Dependências de Desenvolvimento
Para manter as dependências isoladas no ambiente local do projeto (sem poluir o escopo global do sistema operacional), executamos:

```bash
# Instalação do ESLint e Prettier
npm install eslint --save-dev
npm install prettier --save-dev

# Instalação dos plugins de integração harmônica
npm install eslint-config-prettier eslint-plugin-prettier --save-dev
```

**Função dos pacotes de integração:**
- `eslint-config-prettier`: Desativa todas as regras do ESLint que conflitam ou são redundantes com a formatação do Prettier.
- `eslint-plugin-prettier`: Executa o Prettier como se fosse uma regra do próprio ESLint, reportando divergências de formatação como alertas ou erros no terminal.

---

## 3. Arquivos de Configuração

### 3.1 Configuração do ESLint (`.eslintrc.json`)
O ESLint foi configurado para analisar JavaScript moderno (ES2021+), com suporte ao ambiente Node.js e browser, incorporando as regras recomendadas e a extensão do Prettier:

```json
{
  "env": {
    "browser": true,
    "es2021": true,
    "node": true
  },
  "extends": [
    "eslint:recommended",
    "plugin:prettier/recommended"
  ],
  "parserOptions": {
    "ecmaVersion": "latest",
    "sourceType": "module"
  },
  "rules": {
    "no-unused-vars": "warn",
    "no-console": "off",
    "eqeqeq": "error",
    "curly": "error"
  }
}
```

### 3.2 Configuração do Prettier (`.prettierrc`)
Conforme solicitado no roteiro da atividade, o arquivo `.prettierrc` define parâmetros claros de formatação:

```json
{
  "semi": true,
  "singleQuote": true,
  "tabWidth": 2,
  "trailingComma": "es5",
  "printWidth": 80
}
```

*Significado das regras:*
- `"semi": true`: Exige ponto e vírgula obrigatório ao final das instruções.
- `"singleQuote": true`: Utiliza aspas simples (`'`) por padrão para strings literais, reservando aspas duplas apenas para HTML/JSX.
- `"tabWidth": 2`: Define a indentação padrão com 2 espaços.

### 3.3 Arquivo de Ignorados (`.eslintignore` e `.prettierignore`)
Evita processamento desnecessário na pasta de bibliotecas compiladas:

```text
node_modules
dist
build
.git
```

### 3.4 Scripts Automatizados no `package.json`
Para simplificar o dia a dia da equipe, foram adicionados scripts no `package.json`:

```json
"scripts": {
  "lint": "eslint .",
  "lint:fix": "eslint . --fix",
  "format": "prettier --write ."
}
```

---

## 4. Demonstração Prática e Testes de Código

### 4.1 Código Inicial Despadronizado (`index.js`)
Criou-se o arquivo de teste com a estrutura irregular indicada no roteiro, contendo espaçamento inconsistente, falta de indentação e omissão de ponto e vírgula:

```javascript
// CÓDIGO INICIAL (Despadronizado e com problemas de formatação)
const sayHello=()=>{
console.log("Olá mundo!")
}
sayHello()
```

---

### 4.2 Execução do ESLint para Diagnóstico
Executou-se a verificação inicial no terminal:

```bash
npx eslint index.js
```

**Diagnóstico emitido no terminal:**
```text
C:\Users\BrunoDeLima\Desktop\IA\FRONT\SEMANA 26\eslint-prettier-project\index.js
  1:15  error  Insert ` `                               prettier/prettier
  1:20  error  Insert ` `                               prettier/prettier
  2:1   error  Insert `  `                              prettier/prettier
  2:13  error  Replace `"Olá mundo!"` with `'Olá mundo!';`  prettier/prettier
  3:2   error  Insert `;`                               prettier/prettier
  4:11  error  Insert `;`                               prettier/prettier

✖ 6 problems (6 errors, 0 warnings)
  6 errors and 0 warnings potentially fixable with the `--fix` option.
```

---

### 4.3 Correção Automática com ESLint e Prettier

1. **Aplicação do `--fix` pelo ESLint:**
   ```bash
   npx eslint index.js --fix
   ```
2. **Garantia de Formatação com Prettier:**
   ```bash
   npx prettier --write index.js
   ```

---

### 4.4 Código Final Padronizado e Formatado

Após a execução das ferramentas, o arquivo `index.js` foi automaticamente refatorado para o padrão rigoroso adotado pela equipe:

```javascript
// CÓDIGO FINAL: 100% Padronizado, Formatado e Livre de Erros
const sayHello = () => {
  console.log('Olá mundo!');
};

sayHello();
```

**Benefícios visíveis:**
- Espaçamento adequado ao redor da arrow function (`const sayHello = () => {`).
- Indentação de exatos 2 espaços no corpo da função.
- Conversão das aspas duplas para aspas simples (`'Olá mundo!'`).
- Ponto e vírgula adicionado ao final das instruções e no encerramento da constante.

---

## 5. Perguntas para Reflexão (Respostas Teórico-Conceituais)

### Pergunta 1: Qual é a principal diferença entre o ESLint e o Prettier?

> **Resposta Fundamentada:**  
> A principal diferença reside no **propósito e na natureza das regras** avaliadas por cada ferramenta:
> 
> - **ESLint (Code Quality & Bug Prevention):** É um linter voltado para a **lógica e integridade do código**. Ele analisa a árvore sintática abstrata (AST) do JavaScript para detectar comportamentos perigosos ou incorretos, tais como variáveis não declaradas, variáveis declaradas mas nunca utilizadas, funções sem retorno, comparações perigosas com `==` em vez de `===`, e violações de escopo. Embora o ESLint possua algumas regras visuais, sua força motriz é a qualidade funcional.
> - **Prettier (Code Formatting):** É um formatador estritamente **estético e opinativo**. O Prettier não se preocupa se uma variável está sendo usada ou se há um bug de lógica; sua única missão é reescrever o código de forma visualmente limpa, ajustando quebras de linha automáticas (respeitando o limite de caracteres por linha), indentação, aspas, espaços entre chaves e parênteses e pontuação.
> 
> Em suma: o **ESLint garante que o código funcione corretamente e com boas práticas**, enquanto o **Prettier garante que todos no time leiam o código sob o mesmo padrão visual**.

---

### Pergunta 2: Por que é importante integrar o Prettier ao ESLint em um projeto?

> **Resposta Fundamentada:**  
> É indispensável integrá-los para **evitar o conflito destrutivo de regras** e **unificar a esteira de desenvolvimento**.
> 
> 1. **Eliminação de Conflitos Cruzados:** Tanto o ESLint quanto o Prettier possuem regras que lidam com formatação (por exemplo, tamanho de tabulação, ponto e vírgula e aspas). Se ambos atuarem isoladamente sem configuração conjunta, o ESLint pode reclamar de uma formatação que o Prettier acabou de aplicar, gerando um ciclo infinito de erros no editor ou no terminal.
> 2. **Desativação Inteligente com `eslint-config-prettier`:** Ao utilizar essa configuração, todas as regras puramente estéticas do ESLint são desligadas, permitindo que o Prettier detenha autoridade absoluta sobre o layout do código, enquanto o ESLint cuida da qualidade técnica.
> 3. **Feedback Unificado no Editor (VS Code / WebStorm) e CI/CD:** Com `eslint-plugin-prettier`, qualquer inconsistência de formatação é exibida diretamente nas marcações do ESLint e corrigida em lote no comando `npm run lint:fix` ou em rotinas automáticas de pré-commit (`lint-staged` com `Husky`). Isso garante que nenhum código desalinhado seja enviado ao repositório remoto.

---

## 6. Conclusão e Registro das Etapas

A implementação combinada do ESLint e Prettier no projeto estabelece uma base sólida de engenharia de software para o time front-end. Os desenvolvedores ganham agilidade, eliminam discussões subjetivas em Code Reviews sobre estilo de formatação e garantem que a base de código permaneça limpa, legível e robusta ao longo de toda a evolução do produto.
