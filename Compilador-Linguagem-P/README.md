# Compilador - Linguagem P

Implementação do **de um compilador** para a linguagem P com análise léxica, sintática e semântica.

## 📋 Descrição

Projeto prático da disciplina **Compiladores** implementando as três fases principais de análise:
- ✅ **Análise Léxica** - Reconhecimento de tokens usando AFD
- ✅ **Análise Sintática** - Validação de estrutura gramatical com tratamento de erros
- ✅ **Análise Semântica** - Verificação de semântica, tabelas de símbolos e ASA

## 🚀 Quick Start

### Pré-requisitos

- **Python 3.x**
- Sem dependências externas (usa apenas biblioteca padrão)

### Uso

#### Opção 1: Jupyter Notebook (Recomendado para Desenvolvimento)
```bash
jupyter notebook code_with_semantic.ipynb
```

## 📦 Dependências

### Obrigatórias
- **Python 3.x** - Linguagem de programação
- Biblioteca padrão do Python (nenhuma dependência externa)

## 📁 Estrutura do Projeto

```
Compilador-Linguagem-P/
├── code.ipynb                          # Notebook Jupyter completo
├── requirements.txt                    # Dependências Python
├── README.md                           # Este arquivo
├── LICENSE                             # Licença MIT
├── AFDs base/                          # Documentação visual dos AFDs
│   ├── afd1.jpeg
│   ├── afd2.jpeg
│   └── afd3.jpeg
├── codigos base da linguagem p/        # Arquivos de teste (.p)
│   ├── calculadora.p
│   ├── lexical_error.p
│   ├── loop_simples.p
│   ├── media.p
│   ├── soma.p
│   └── tokens.p
├── saidas do analisador sintatico/     # Saída: Erros sintáticos (TXT)
├── tabelas de simbolos/                # Saída: Tabelas de símbolos (TXT)
└── saidas do analisador semantico/     # Saída: ASA (JSON) + Erros semânticos (TXT)
```

## 🔍 Como Funciona

### Fluxo de Compilação

```
Arquivo .p
    ↓
┌─────────────────────┐
│ Análise Léxica      │ → Reconhece tokens usando AFD
└─────────────────────┘
    ↓
┌─────────────────────┐
│ Análise Sintática   │ → Valida gramática com recuperação de erros
└─────────────────────┘
    ↓
┌─────────────────────┐
│ Análise Semântica   │ → Constrói ASA e tabelas de símbolos
└─────────────────────┘
    ↓
┌──────────────────────────────────────────────┐
│ Saídas Geradas:                              │
│ • Erros sintáticos                           │
│ • Tabela de símbolos                         │
│ • Árvore de Sintaxe Abstrata (ASA)           │
│ • Erros semânticos                           │
└──────────────────────────────────────────────┘
```

## 💻 Compilando um Arquivo

## 📊 Saídas Geradas

Para cada arquivo compilado, são gerados **4 arquivos**:

### 1. Erros Sintáticos (TXT)
**Local**: `saidas do analisador sintatico/{arquivo}_syntax.txt`

```txt
Arquivo: soma.p
Status: VÁLIDO
Não foram encontrados erros sintáticos.
```

### 2. Tabelas de Símbolos (TXT)
**Local**: `tabelas de simbolos/{arquivo}_tabelas.txt`

```txt
TABELA DE SÍMBOLOS: soma
────────────────────────────────────────────────────────────────
Chave           Nome            Tipo         Parâmetro  Pos_Param
────────────────────────────────────────────────────────────────
soma            soma            function     Não        -1
x               x               int          Sim        0
y               y               int          Sim        1

ret_type(soma): int
```

### 3. Árvore de Sintaxe Abstrata (JSON)
**Local**: `saidas do analisador semantico/{arquivo}_ast.json`

```json
{
  "arquivo": "soma.p",
  "funcoes": {
    "soma": {
      "tipo": "function",
      "valor": "soma",
      "tipo_dado": "int",
      "filhos": []
    },
    "main": {
      "tipo": "function",
      "valor": "main",
      "tipo_dado": null,
      "filhos": []
    }
  }
}
```

### 4. Erros Semânticos (TXT)
**Local**: `saidas do analisador semantico/{arquivo}_semantic.txt`

```txt
Arquivo: soma.p
Status: VÁLIDO
Não foram encontrados erros semânticos.
```

## 🔍 Exemplo de Uso

### Arquivo de entrada: `soma.p`

```p
fn soma(x: int, y: int) -> int {
    return x + y;
}

fn main() {
    let a, b, c: int;
    b = 40;
    c = 39;
    a = soma(b, c);
    println("{}", a);
}
```

### Executar compilador

Completar aqui 

### Saídas geradas

**soma_syntax.txt**
```
Status: VÁLIDO
Não foram encontrados erros sintáticos.
```

**soma_tabelas.txt**
```
TABELA DE SÍMBOLOS: soma
────────────────────────────────────────────
Chave    Nome    Tipo      Parâmetro  Pos_Param
────────────────────────────────────────────
soma     soma    function  Não        -1
x        x       int       Sim        0
y        y       int       Sim        1
ret_type(soma): int

TABELA DE SÍMBOLOS: main
────────────────────────────────────────────
Chave    Nome    Tipo      Parâmetro  Pos_Param
────────────────────────────────────────────
main     main    function  Não        -1
a        a       int       Não        -1
b        b       int       Não        -1
c        c       int       Não        -1
println  println function  Não        -1
ret_type(main): void
```

## 🛠️ Tratamento de Erros

### Erro Léxico
Caractere não reconhecido pelo AFD
```
Erro léxico: caractere inesperado '$' na linha 5
```

### Erro Sintático
Violação da gramática da linguagem
```
Arquivo: lexical_error.p
Status: INVÁLIDO - 1 erro(s) encontrado(s)

ERROS SINTÁTICOS:
Linha 6: Esperado 'RBRACKET', encontrado 'FMT_STRING'
```

### Erro Semântico
Violação de regras semânticas (variáveis não declaradas, duplicação, etc)
```
Arquivo: erro.p
Status: INVÁLIDO - 2 erro(s) encontrado(s)

ERROS SEMÂNTICOS:
Linha 5: Variável 'x' não declarada
Linha 7: Variável 'y' já declarada
```

## 📚 Classes Principais

| Classe | Descrição |
|--------|-----------|
| `Token` | Representa um token léxico com tipo, valor e linha |
| `AFD` | Autômato Finito Determinístico para reconhecimento de lexemas |
| `Lexer` | Analisador léxico que usa AFD para gerar tokens |
| `ASTNode` | Nó da Árvore de Sintaxe Abstrata |
| `Symbol` | Representa um identificador na tabela de símbolos |
| `SymbolTable` | Tabela de símbolos de uma função/escopo |
| `SymbolTableManager` | Gerencia múltiplas tabelas de símbolos |
| `Parser` | Analisador sintático e semântico |

## 📝 Gramática da Linguagem P

```
Programa → Função Programa'
Programa' → Função Programa' | ε

Função → fn NomeFunção ( ListaParams ) [→ Tipo] { Sequência }
NomeFunção → ID | main
Tipo → int | float | char

ListaParams → [ID : Tipo (COMMA ID : Tipo)*] 

Sequência → (Declaração | Comando)*

Declaração → let VarList : Tipo ;
VarList → ID (COMMA ID)*

Comando → ID = Expr ;                    // Atribuição
         | ID ( ListaArgs ) ;            // Chamada de função
         | if Expr { Sequência } ComandoSenão
         | while Expr { Sequência }
         | println ( FMT_STRING , Expr ) ;
         | return Expr ;

ComandoSenão → else (if Expr { Sequência } ComandoSenão | { Sequência }) | ε

Expr → Rel ExprOpc
ExprOpc → (== | !=) Rel ExprOpc | ε

Rel → Adição RelOpc
RelOpc → (< | <= | > | >=) Adição RelOpc | ε

Adição → Termo AdicaoOpc
AdicaoOpc → (+ | -) Termo AdicaoOpc | εatualização**: Dezembro 10, 2025
**Status**: ✅ Funcional com teste completo

Termo → Fator TermoOpc
TermoOpc → (* | /) Fator TermoOpc | ε

Fator → ID [( ListaArgs )]             // Variável ou chamada de função
       | INT_CONST
       | FLOAT_CONST
       | CHAR_LITERAL
       | ( Expr )

ListaArgs → [Expr (COMMA Expr)*]
```

## 🎯 Palavras Reservadas

| Palavra | Tipo | Descrição |
|---------|------|-----------|
| `fn` | FUNCTION | Declaração de função |
| `main` | MAIN | Função principal |
| `let` | LET | Declaração de variáveis |
| `int` | INT | Tipo inteiro |
| `float` | FLOAT | Tipo ponto flutuante |
| `char` | CHAR | Tipo caractere |
| `if` | IF | Condicional |
| `else` | ELSE | Condicional alternativa |
| `while` | WHILE | Loop |
| `return` | RETURN | Retorno de função |
| `println` | PRINTLN | Impressão de saída |

## 📖 Arquivos de Teste

A pasta `codigos base da linguagem p/` contém exemplos de programas na linguagem P:

- **soma.p** - Função com parâmetros e retorno
- **media.p** - Cálculos com floats
- **loop_simples.p** - Loop com while
- **calculadora.p** - Comandos condicionais aninhados
- **lexical_error.p** - Exemplo com erros léxicos/sintáticos
- **tokens.p** - Demonstração de todos os tokens

## 🔧 Desenvolvimento

### Adicionar novo arquivo de teste

1. Criar arquivo `.p` em `codigos base da linguagem p/`
2. Adicionar à lista `arquivos` em `compilar_arquivo()`
3. Executar o compilador
4. Verificar saídas nas respectivas pastas

### Modificar regras semânticas

Editar métodos em `Parser`:
- `parse_declaracao()` - Declarações de variáveis
- `parse_comando()` - Comandos e expressões
- `_generate_semantic_errors()` - Geração de erros semânticos

### Adicionar novos tokens

1. Modificar `make_afd()` - Transições do AFD
2. Adicionar palavras reservadas em `Lexer.tokenize()`
3. Atualizar produções no `Parser`

## 📊 Resultados dos Testes

| Arquivo | Status Sintático | Status Semântico | Funções | Variáveis |
|---------|------------------|------------------|---------|-----------|
| soma.p | ✅ Válido | ✅ Válido | 2 | 6 |
| media.p | ✅ Válido | ✅ Válido | 1 | 5 |
| loop_simples.p | ✅ Válido | ✅ Válido | 1 | 2 |
| calculadora.p | ✅ Válido | ✅ Válido | 2 | 4 |
| lexical_error.p | ❌ Inválido | ✅ Válido | 1 | 4 |

## 🏗️ Arquitetura

### Fluxo de Dados

```
┌─────────────────────────────────────────────────────┐
│              Arquivo .p (Entrada)                   │
└────────────────┬────────────────────────────────────┘
                 │
                 ▼
        ┌─────────────────┐
        │   Lexer (AFD)   │
        │ Análise Léxica  │
        └────────┬────────┘
                 │
            ┌────▼─────┐
            │  Tokens   │
            └────┬─────┘
                 │
        ┌────────▼────────────┐
        │  Parser (Sintático) │
        │  Análise Sintática  │
        └────────┬────────────┘
                 │
         ┌───────┴────────┐
         │                │
    ┌────▼────┐    ┌──────▼──────┐
    │   ASA   │    │Symbol Tables │
    └────┬────┘    └──────┬──────┘
         │                │
         └────────┬───────┘
                  │
     ┌────────────▼─────────────┐
     │   Geração de Saídas      │
     │ • .txt (erros/símbolos)  │
     │ • .json (ASA)            │
     └──────────────────────────┘
```

## 🔐 Recursos de Tratamento de Erros

✅ **Recuperação de erro** - O compilador continua analisando após encontrar erros
✅ **Sincronização** - Retorna a parsing em pontos seguros após erros
✅ **Relatórios detalhados** - Número da linha e descrição de cada erro
✅ **Validação semântica** - Detecta variáveis não declaradas e duplicadas

## 📄 Licença

MIT License - veja [LICENSE](LICENSE) para detalhes

## 👥 Autores

- **Arthur Henrique** - Implementação
- **André Luiz** - Implementação

## 📚 Referências

- Disciplina: Compiladores
- Linguagem de Implementação: Python 3.x
- Data: Dezembro de 2025

---

**Última atualização**: Dezembro 10, 2025
**Status**: ✅ Funcional com teste completo