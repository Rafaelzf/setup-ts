# Setup básico ReactJs + TypeScript + StyledComponents

> Projeto usando `create-react-app` + `typescript` + `editor config` + `ESlint` +`Prettier` + `husk` e `lint-staged` + `stylelint`

## Create react app

```sh
npx create-react-app style-guide --template typescript
```

## Editor config

```sh
root = true // verdadeiro para arquivo no pasta root do projeto

[*]
indent_style = tab 	//identação por tab
indent_size = 2 	// soft tabs
charset = utf-8 	//padrão para alfabeto latino
end_of_line = lf 	//ir para a próxima linha
trim_trailing_whitespace = true 	// não permitir espaço em branco ao fim da lina
insert_final_newline = true		// ao fim da linha, pular para próxima automaticamente
```

- [https://editorconfig.org/](https://editorconfig.org/)
- [https://editorconfig-specification.readthedocs.io/en/latest/](https://editorconfig-specification.readthedocs.io/en/latest/)

## ESlint

```sh
yarn add eslint -D
```

> Se estiver usando create-react-app para inicializar um projeto, eslint já está incluído como uma dependência por meio de `react-script` se, portanto, não é necessário instalá-lo explicitamente com yarn.

```sh
yarn run eslint --init
```

1. **How would you like to use ESLint?**
   1. To check syntax, find problems, and enforce code style
2. **What type of modules does your project use?**
   1. JavaScript modules (import/export)
3. **Which framework does your project use?**
   1. React
4. **Does your project use TypeScript?**
   1. yes
5. **Where does your code run?**
   1. Browser
6. **How would you like to define a style for your project?**
   1. Use a popular style guide
      1. Airbnb: [https://github.com/armoucar/javascript-style-guide](https://github.com/armoucar/javascript-style-guide)
7. **What format do you want your config file to be in?**
   1. JSON
8. **Would you like to install them now with npm?**
   1. No (se quiser usar o yarn)

## Dependências necessárias

`eslint-plugin-react`

`@typescript-eslint/eslint-plugin`

`eslint-config-airbnb`

`eslint-config-airbnb-typescript`

`eslint`

`eslint-plugin-import`

`eslint-plugin-jsx-a11y`

`eslint-plugin-react-hooks`

`@typescript-eslint/parser`

```sh
yarn add eslint-plugin-react@^7.19.0 @typescript-eslint/eslint-plugin@latest eslint-config-airbnb@latest eslint-plugin-import@^2.20.1 eslint-plugin-jsx-a11y@^6.2.3 eslint-plugin-react-hooks@^2.5.0 @typescript-eslint/parser@latest -D
```

## O que são

- **eslint:** A principal biblioteca de linting ESLint.
- **eslint-plugin-react:** Conjunto de regras para o ESlint aplicar à sintaxe do React.
- **eslint-config-airbn**: Conjunto de boas práticas para códigos feitos em ES6
- **@typescript-eslint/parser**: O analisador que permitirá que o ESLint aplique regras ao código TypeScript.
- **@typescript-eslint/eslint-plugin:** Um plugin que contém várias regras ESLint que são específicas do TypeScript.
- **eslint-plugin-react-hooks**: Regras para aplicação em React Hooks.
- **eslint-plugin-jsx-a11**: Regras de aplicação em JSX.

## Documentação de cada uma

- [eslint-plugin-react](https://www.npmjs.com/package/eslint-plugin-react)
- [@typescript-eslint/eslint-plugin](https://www.npmjs.com/package/@typescript-eslint/eslint-plugin)
- [eslint-config-airbnb](https://www.npmjs.com/package/eslint-config-airbnb)
- [eslint-config-airbnb-typescript](https://www.npmjs.com/package/eslint-config-airbnb-typescript)
- [eslint](https://www.npmjs.com/package/eslint)
- [eslint-plugin-import](https://www.npmjs.com/package/eslint-plugin-import)
- [eslint-plugin-jsx-a11y](https://github.com/jsx-eslint/eslint-plugin-jsx-a11y)
- [@typescript-eslint/parser](https://www.npmjs.com/package/@typescript-eslint/parser)

## No seu arquivo de configuração ESLint:

```sh
{
  "env": {
    "browser": true,
    "es6": true
  },
  "extends": ["plugin:react/recommended", "airbnb"],
  "parser": "@typescript-eslint/parser", // Especifica o analisador ESLint

  "parserOptions": {
    "ecmaFeatures": {
      "jsx": true // Permite a análise de JSX
    },
    "ecmaVersion": 12, // Permite a análise de recursos modernos do ECMAScript
    "sourceType": "module" // Permite o uso de importações
  },
  "settings": {
    "react": {
      "version": "detect" // Diz ao eslint-plugin-react para detectar automaticamente a versão do React a usar
    }
  },
  "plugins": [
    "react",
    "@typescript-eslint" // Usa as regras recomendadas de @ typescript-eslint / eslint-plugin
  ],
  "rules": {
    // Local para especificar regras ESLint. Pode ser usado para substituir as regras especificadas nas configurações estendidas
    // por exemplo, "@ typescript-eslint / explicit-function-return-type": "off",
  }
}

```

## Em seguida, instale os pacotes para configuração do Airbnb. Este comando funcionará para Yarn ou NPM

```sh
npx install-peerdeps --dev eslint-config-airbnb
```

## Adicionando Prettier

```sh
`yarn add -D prettier`

`yarn add -D eslint-config-prettier`

`yarn add -D eslint-plugin-prettier`
```

ou

```sh
yarn add -D prettier eslint-config-prettier eslint-plugin-prettier
```

## O que são

- **prettier**: Um formatador de código opinativo
- **eslint-config-prettier**: Desativa as regras ESLint que podem entrar em conflito com o **prettier**
- **eslint-plugin-prettier**: Faz o **prettier** funcionar como uma regra ESLint.

Para uma configuração do prettier, é necessário um arquivo no diretório raiz do projeto chamado `sh prettier.config.js`

```sh
export const singleQuote = true; //Aspas simples
export const trailingComma = 'all'; //Para adicionar a ultima vírgula no final dos objetos e arrays
export const semi  = true; // ponto final ao fim do comando
export const tabWidth = 2; //tamanho do tab
```

ou

```sh
{
	(singleQuote = true), (trailingComma = "all"), (semi = true), (tabWidth = 2);
}
```

O próximo passo é editar as regras que o ESLint irá avaliar. Entre as regras temos a permissão de código JSX dentro de arquivos .tsx e permissão de importação de arquivos .ts e .tsx sem declarar explicitamente a extensão. Você pode consultar mais regras no link, e pode alterar durante o desenvolvimento. Porém, cuidado com muitas modificações para não criar inconsistências no código.

Para resolver as importações com Typescript primeiro devemos adicionar a dependência abaixo:

```sh
yarn add eslint-import-resolver-typescript -D
```

```sh
	"rules": {
		"prettier/prettier": "error",
		"react-hooks/rules-of-hooks": "error",
		"react-hooks/exhaustive-deps": "warn",
		"react/jsx-filename-extension": [
			"error",
			{ "extensions": [".js", ".jsx", ".ts", ".tsx"] }
		],
		"import/prefer-default-export": "off",
		"@typescript-eslint/explicit-function-return-type": [
			"error",
			{ "allowExpressions": true }
		],
		"import/extensions": [
			"error",
			"ignorePackages",
			{ "ts": "never", "tsx": "never" }
		],
		"no-unused-expressions": ["error", { "allowTaggedTemplates": true }]
	},
```

E por fim, para resolver as importações com Typescript adicionamos a seguinte configuração.

```sh
"settings": {
		"import/resolver": {
			"typescript": {}
		}
	}
```

## Configurando ESLint e Prettier

Primeiramente criamos um arquivo `sh .eslintignore `, que inclui os arquivos onde o ESLint não irá visualizar.

```sh
**/*.js
node_modules
build
```

## Em seguida, o `.eslintrc.js ` precisa ser atualizado:

```sh
{
	"env": {
		"browser": true,
		"es2021": true,
		"jest": true
	},
	"extends": [
		"airbnb-typescript",
		"airbnb/hooks",
		"plugin:@typescript-eslint/recommended",
		"plugin:jest/recommended",
		"prettier",
		"prettier/react",
		"prettier/@typescript-eslint",
		"plugin:prettier/recommended"
	],
	"parser": "@typescript-eslint/parser",
	"parserOptions": {
		"ecmaFeatures": {
			"jsx": true
		},
		"ecmaVersion": 12,
		"sourceType": "module",
		"project": "./tsconfig.json"
	},
	"plugins": ["react", "@typescript-eslint", "jest", "prettier", "react-hooks"],

	"rules": {
		"prettier/prettier": "error",
		"react-hooks/rules-of-hooks": "error",
		"react-hooks/exhaustive-deps": "warn",
		"react/jsx-filename-extension": [
			"error",
			{ "extensions": [".js", ".jsx", ".ts", ".tsx"] }
		],
		"import/prefer-default-export": "off",
		"@typescript-eslint/explicit-function-return-type": [
			"error",
			{ "allowExpressions": true }
		],
		"import/extensions": [
			"error",
			"ignorePackages",
			{ "ts": "never", "tsx": "never" }
		],
		"no-unused-expressions": ["error", { "allowTaggedTemplates": true }]
	},

	"settings": {
		"import/resolver": {
			"typescript": {}
		}
	}
}
```

> Certifique-se de que esta plugin:prettier/recommended é a última configuração no extends array

A vantagem de ter uma configuração prettier como uma regra ESLint usando `eslint-plugin-prettier` é que o código pode ser corrigido automaticamente usando a `--fix` opção ESLint .

## Corrigir automaticamente o código no código do VS

É útil configurar seu editor para executar automaticamente o comando de correção automática do ESLint (ou seja, `eslint --fix`) sempre que um arquivo for salvo. Como estou usando o VS Code, aqui está a configuração necessária no arquivo `settings.json` do VS Code:

```sh
{
  "editor.codeActionsOnSave" : {
    "source.fixAll.eslint" : true
  } ,
}

// e para Typescript

"[typescript]": {
    "editor.codeActionsOnSave": {
      "source.fixAll.eslint": true
    }
  },
```

## Execute ESLint com o CLI

```sh
{
  "scripts" : {
    "lint": "eslint ./src --ext .js,.ts,.tsx,.json",
		"lint:fix": "eslint ./src --ext .js,.ts,.tsx,.json --fix"
  }
}
```

> Este comando será executado ESLint por todos arquivos .js, .tse .tsx (usado com React). Quaisquer erros de ESLint que possam ser corrigidos automaticamente serão corrigidos com este comando, mas quaisquer outros erros serão impressos na linha de comando.

## Opções ESLint CLI

> Mesmo que o ESLint não relate nenhum erro, isso não significa necessariamente que o compilador TypeScript não relatará nenhum erro de tipo. Para verificar se o seu código contém erros de tipo, é uma boa usar o comando tsc `--noEmit`.

## Execute Prettier com o CLI

```sh
  {
    "scripts" : {
      "lint": "eslint \"./src/**/*.{ts,js,tsx,jsx}\" -f table",
      "lint:fix": "eslint ./src --ext .js,.ts,.tsx --fix",
    }
  }
}
```

## Instalando lint-staged (husky)

Lint-staged é uma ferramenta que aplica um lint (`ESlint`) mais o `Prettier` na área de staged, ou seja, no local e nos arquivos modificados após o git add. Isso previne que o lint e o prettier percorram todos os arquivos de forma desnecessária, já que apenas os arquivos modificados deverão ser analisados.

- [Husk](https://github.com/typicode/husky)

Crie um propriedade em seu `package.json`

```sh
{
  "husky": {
    "hooks": {
      "pre-commit": "pretty-quick --staged"
    }
  }
}
```

## Instale o lint-staged

`yarn add lint-staged -D`

Crie um propriedade em seu `package.json`

```sh
"lint-staged": {
    "*.{ts,js,tsx,jsx}": [
      "eslint",
      "git add"
    ]
  },
```

Agora altere o husky para rodar o `lint-staged`

```sh
"husky": {
    "hooks": {
      "pre-commit": "lint-staged",
      "pre-push": "yarn lint:fix"
    }
  },
```

## StyledComponents

O styled-components é um package que permite você estilizar seus componentes dentro do React escrevendo CSS dentro do seu arquivo JS/TS do mesmo jeito que se estivesse em um arquivo com extensão “.css”.

`yarn add styled-components`

Este erro é causado pois não instalamos o [package de definição](https://www.npmjs.com/package/@types/styled-components) de tipos do `styled-components`, com ele conseguiremos utilizar o _intellisense_ do _VS Code_, então para isso devemos executar em nosso terminal na raiz do projeto:

`yarn add @types/styled-components -D`

## Stylelint

Um linter poderoso e moderno que o ajuda a evitar erros e a aplicar convenções em seus estilos.

**Você vai precisar:**

- O `stylelint-processor-styled-components`, para extrair estilos do `styled-components`.
- O `stylelint-config-styled-components` para desabilitar as regras do `stylelint` que conflitam com o `styled-components`.
- Uma configuração padrão para `stylelint` (por exemplo: `stylelint-config-recommended`).

> É aconselhável o uso de Stylelint v9 +, pois ele adicionou recursos que nos permitem relatar números de linha corretos em erros de sintaxe CSS.

```sh
yarn add stylelint -D

yarn add stylelint-processor-styled-components -D

yarn add stylelint-config-styled-components -D

yarn add stylelint-config-recommended -D
```

Adicione o arquivo de configuração `.stylelintrc` na raiz do projeto

```sh
{
  "processors": [
    "stylelint-processor-styled-components"
  ],
  "extends": [
    "stylelint-config-recommended",
    "stylelint-config-styled-components"
  ]
}
```

Quando precisar rodar o `stylelint`, adicione em seus scripts no `package.json`

```sh

{
  "scripts": {
      "lint:css": "stylelint \"./src/**/style.ts\" --color -f verbose"
  }
}
```

Agora é preciso alterar seu `lint-staged`

```sh
"lint-staged": {
    "*.{ts,js,tsx,jsx}": [
      "eslint -f table"
    ],
    "*style.ts": [
      "stylelint --color -f verbose"
    ]
  },
```
