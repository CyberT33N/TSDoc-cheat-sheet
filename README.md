# TSDoc-cheat-sheet

# Links
- https://github.com/microsoft/tsdoc
- https://tsdoc.org/







<br><br>

---

<br><br>



# Install

<details><summary>Click to expand..</summary>

```shell
npm install --save-dev eslint-plugin-tsdoc
```

<br><br>

eslint.config.mjs
```shell
// ==== Imports ====
import eslint from '@eslint/js'
import importPlugin from 'eslint-plugin-import'
import a11yPlugin from 'eslint-plugin-jsx-a11y'
import reactPlugin from 'eslint-plugin-react'
import reactHooksPlugin from 'eslint-plugin-react-hooks'
import tsdocPlugin from 'eslint-plugin-tsdoc'
import tseslint from 'typescript-eslint'

export default tseslint.config(
    {
        // Global ignores for other directories, but not for eslint.config.mjs itself regarding naming conventions
        ignores: ['eslint.config.mjs', 'coverage/**']
    },
    // ===== ESLINT BASE RULES =====
    eslint.configs.recommended,
    
    // ===== TYPESCRIPT-ESLINT CONFIGURATIONS =====
    // Include ALL strict TypeScript rules (includes recommended)
    tseslint.configs.strictTypeChecked,
    tseslint.configs.stylisticTypeChecked,
    
    // ===== ESLINT CORE RULES CUSTOMIZATION =====
    {
        rules: {
            'arrow-parens': ['error', 'as-needed'],
            'no-var': 'error',
            'no-eval': 'error',
            'indent': ['error', 4],
            'quotes': ['error', 'single'],
            'no-console': ['error', { allow: ['warn', 'error', 'info', 'trace' ] }], // Stricter than original
            'space-before-function-paren': ['error', 'never'],
            'padded-blocks': ['error', 'never'],
            'prefer-arrow-callback': ['error', { // Stricter than original
                allowNamedFunctions: true
            }],
            'func-names': ['error', 'never'],
            'no-use-before-define': 'off', // Let typescript-eslint handle this
            'max-len': ['error', 120],
            'object-curly-spacing': ['error', 'always'], // Stricter than original
            'comma-dangle': ['error', 'never'],
            'semi': ['error', 'never'],
            'new-cap': ['error', { // Stricter than original
                newIsCap: true,
                capIsNew: false
            }],
            'one-var': ['error', 'never'], // Stricter than original
            'guard-for-in': 'error', // Stricter than original
            'no-duplicate-imports': 'error',
            'no-return-await': 'error',
            'no-template-curly-in-string': 'error',
            'require-atomic-updates': 'error',
            'accessor-pairs': 'error',
            'array-callback-return': 'error',
            'block-scoped-var': 'error',
            'camelcase': ['error', { properties: 'never' }],
            'complexity': ['error', 20],
            'consistent-return': 'error',
            'curly': ['error', 'all'],
            'default-case': 'error',
            'eqeqeq': ['error', 'always'],
            'dot-notation': 'off' // Disabled to allow bracket notation for private method testing
        }
    },
    
    // ===== IMPORT PLUGIN =====
    {
        plugins: {
            import: importPlugin
        },
        settings: {
            'import/parsers': {
                '@typescript-eslint/parser': ['.ts', '.tsx']
            },
            'import/resolver': {
                typescript: {
                    alwaysTryTypes: true,
                    project: './tsconfig.json',
                    extensions: ['.ts', '.tsx', '.js', '.jsx'],
                    paths: {
                        '@main/*': ['./src/main/*'],
                        '@/*': ['./src/*']
                    }
                },
                node: {
                    extensions: ['.ts', '.tsx', '.js', '.jsx'],
                    paths: ['src']
                }
            }
        },
        rules: {
            'import/first': 'error',
            'import/no-duplicates': 'error',
            'import/order': ['error', {
                'groups': [
                    'builtin',
                    'external',
                    'internal',
                    'parent',
                    'sibling',
                    'index'
                ],
                'alphabetize': {
                    'order': 'asc',
                    'caseInsensitive': true
                }
            }],
            'import/no-unresolved': 'error',
            'import/no-cycle': 'error',
            'import/no-unused-modules': 'error'
        }
    },
    
    // ===== REACT RULES =====
    {
        plugins: {
            react: reactPlugin,
            'react-hooks': reactHooksPlugin,
            'jsx-a11y': a11yPlugin
        },
        languageOptions: {
            parserOptions: {
                ecmaFeatures: {
                    jsx: true
                }
            }
        },
        settings: {
            react: {
                version: 'detect'
            }
        },
        rules: {
            // React rules
            'react/react-in-jsx-scope': 'off',
            'react/prop-types': 'off',
            'react-hooks/rules-of-hooks': 'error',
            'react-hooks/exhaustive-deps': 'error', // Stricter than original
            'react/no-access-state-in-setstate': 'error',
            'react/no-array-index-key': 'error',
            'react/no-danger': 'error',
            'react/no-did-mount-set-state': 'error',
            'react/no-did-update-set-state': 'error',
            'react/no-direct-mutation-state': 'error',
            'react/no-redundant-should-component-update': 'error',
            'react/no-typos': 'error',
            'react/no-this-in-sfc': 'error',
            'react/no-unescaped-entities': 'error',
            'react/no-unknown-property': 'error',
            'react/no-unused-state': 'error',
            'react/no-will-update-set-state': 'error',
            'react/prefer-es6-class': ['error', 'always'],
            'react/prefer-stateless-function': 'error',
            'react/self-closing-comp': 'error',
            'react/sort-comp': 'error',
            'react/jsx-no-bind': ['error', {
                'allowArrowFunctions': true
            }],
            'react/jsx-no-useless-fragment': 'error',
            'react/jsx-pascal-case': 'error',
            
            // A11y rules
            'jsx-a11y/alt-text': 'error',
            'jsx-a11y/anchor-has-content': 'error',
            'jsx-a11y/anchor-is-valid': 'error',
            'jsx-a11y/aria-props': 'error',
            'jsx-a11y/aria-role': 'error',
            'jsx-a11y/heading-has-content': 'error',
            'jsx-a11y/no-autofocus': 'error',
            'jsx-a11y/no-redundant-roles': 'error'
        }
    },
    
    // ===== TYPESCRIPT PARSER CONFIG =====
    {
        languageOptions: {
            parser: tseslint.parser,
            parserOptions: {
                /*
                - https://typescript-eslint.io/blog/announcing-typescript-eslint-v8/#project-service
                The project service will automatically find the closest tsconfig.json for each file (like project: true)
                */
                projectService: true,

                /* 
                - https://typescript-eslint.io/packages/parser/#tsconfigrootdir
                The root directory for the tsconfig.json file (https://typescript-eslint.io/packages/parser/#tsconfigrootdir) */
                tsconfigRootDir: import.meta.dirname
            }
        }
    },
    
    // ===== ADDITIONAL TYPESCRIPT RULES =====
    {
        rules: {
            // Additional typescript-eslint rules not included in strict
            '@typescript-eslint/explicit-function-return-type': 'error',
            '@typescript-eslint/explicit-member-accessibility': 'error',
            '@typescript-eslint/member-ordering': 'error',
            '@typescript-eslint/dot-notation': 'off', // Disabled to allow bracket notation for private method testing
            '@typescript-eslint/naming-convention': [
                'error',
                {
                    'selector': 'default',
                    'format': ['camelCase']
                },
                {
                    'selector': 'variable',
                    'format': ['camelCase', 'UPPER_CASE']
                },
                {
                    'selector': 'parameter',
                    'format': ['camelCase'],
                    'leadingUnderscore': 'allow'
                },
                {
                    'selector': 'memberLike',
                    'modifiers': ['private'],
                    'format': ['camelCase'],
                    'leadingUnderscore': 'require'
                },
                {
                    'selector': 'typeLike',
                    'format': ['PascalCase']
                },
                {
                    'selector': 'interface',
                    'format': ['PascalCase'],
                    'prefix': ['I']
                },
                {
                    'selector': 'enum',
                    'format': ['PascalCase'],
                    'prefix': ['E']
                },
                // ANPASSUNG FÜR OBJEKT-PROPERTIES (wie _errors oder Zods required_error)
                {
                    'selector': ['objectLiteralProperty', 'typeProperty'], // Gilt für Properties in Objektliteralen und Typdefinitionen
                    'format': ['camelCase', 'snake_case', 'PascalCase'], // Erlaube verschiedene Formate
                    'leadingUnderscore': 'allow' // WICHTIG: Erlaube hier führende Unterstriche
                // Optional: Wenn du es *nur* für spezifische Namen wie '_errors' erlauben willst:
                // 'filter': { 'regex': '^_errors$', 'match': true }
                // Aber 'allow' ist oft einfacher, wenn mehrere solcher Fälle von externen Bibliotheken kommen.
                }
            ],
            '@typescript-eslint/no-explicit-any': 'error',
            '@typescript-eslint/no-non-null-assertion': 'error',
            '@typescript-eslint/no-unnecessary-condition': 'error',
            '@typescript-eslint/prefer-optional-chain': 'error',
            '@typescript-eslint/prefer-nullish-coalescing': 'error',
            '@typescript-eslint/prefer-readonly': 'error',
            '@typescript-eslint/prefer-readonly-parameter-types': 'error',
            '@typescript-eslint/require-array-sort-compare': 'error',
            '@typescript-eslint/strict-boolean-expressions': 'error',
            '@typescript-eslint/switch-exhaustiveness-check': 'error',
            '@typescript-eslint/restrict-template-expressions': 'error',
            '@typescript-eslint/unbound-method': 'error',
            '@typescript-eslint/no-floating-promises': 'error',
            '@typescript-eslint/promise-function-async': 'error',
            '@typescript-eslint/prefer-enum-initializers': 'error',
            '@typescript-eslint/prefer-literal-enum-member': 'error'
        }
    },
    
    // ===== TSDOC PLUGIN =====
    {
        plugins: {
            tsdoc: tsdocPlugin
        },
        rules: {
            'tsdoc/syntax': 'error'
        }
    }
)
```

</details>











<br><br>

---

<br><br>



# Syntax

<details><summary>Click to expand..</summary>

<br><br>

# declaration references 
- The "new" syntax for declaration references is described in this grammar:
- https://github.com/microsoft/tsdoc/blob/main/tsdoc/src/beta/DeclarationReference.grammarkdown

<details><summary>Click to expand..</summary>

```plaintext
//
// Lexical Grammar
//

SourceCharacter::
  > Any unicode code point

WhiteSpace::
  <TAB>
  <VT>
  <FF>
  <SP>
  <NBSP>
  <ZWNBSP>
  <USP>

LineTerminator::
  <LF>
  <CR>
  <LS>
  <PS>

// MeaningKeyword represents each of the possible meanings of a TypeScript symbol, 
// in addition to some custom types.
MeaningKeyword: one of
  `class`                                       // SymbolFlags.Class
  `interface`                                   // SymbolFlags.Interface
  `type`                                        // SymbolFlags.TypeAlias
  `enum`                                        // SymbolFlags.Enum
  `namespace`                                   // SymbolFlags.Module
  `function`                                    // SymbolFlags.Function
  `var`                                         // SymbolFlags.Variable
  `constructor`                                 // SymbolFlags.Constructor
  `member`                                      // SymbolFlags.ClassMember | SymbolFlags.EnumMember
  `event`                                       //
  `call`                                        // SymbolFlags.Signature (for __call)
  `new`                                         // SymbolFlags.Signature (for __new)
  `index`                                       // SymbolFlags.Signature (for __index)
  `complex`                                     // Any complex type

Punctuator:: one of
  `{` `}` `(` `)` `[` `]` `!` `.` `#` `~` `:` `,`

FutureReservedPunctuator:: one of
  `{` `}` `@`

NavigationPunctuator: one of
  `.`                                           // Navigate via 'exports' of symbol
  `#`                                           // Navigate via 'members' of symbol
  `~`                                           // Navigate via 'locals' of symbol

DecimalDigits::
  DecimalDigit
  DecimalDigits DecimalDigit

DecimalDigit:: one of
  `0` `1` `2` `3` `4` `5` `6` `7` `8` `9`

HexDigits::
  HexDigit HexDigits?

HexDigit:: one of
  `0` `1` `2` `3` `4` `5` `6` `7` `8` `9` `a` `b` `c` `d` `e` `f` `A` `B` `C` `D` `E` `F`

String::
  `"` StringCharacters? `"`

StringCharacters::
  StringCharacter StringCharacters?

StringCharacter::
  SourceCharacter but not one of `"` or `\` or LineTerminator
  `\` EscapeSequence

EscapeSequence::
  CharacterEscapeSequence
  `0` [lookahead != DecimalDigit]
  HexEscapeSequence
  UnicodeEscapeSequence

CharacterEscapeSequence::
  SingleEscapeCharacter
  NonEscapeCharacter

SingleEscapeCharacter:: one of
  `'` `"` `\` `b` `f` `n` `r` `t` `v`

NonEscapeCharacter::
  SourceCharacter but not one of EscapeCharacter or LineTerminator

EscapeCharacter::
  SingleEscapeCharacter
  DecimalDigit
  `x`
  `u`

HexEscapeSequence::
  `x` HexDigit HexDigit

UnicodeEscapeSequence::
  `u` Hex4Digits
  `u` `{` CodePoint `}`

Hex4Digits::
  HexDigit HexDigit HexDigit HexDigit

CodePoint::
  > |HexDigits| but only if MV of |HexDigits| ≤ 0x10FFFF

// Represents the path for a module
ModuleSource::
  String
  ModuleSourceCharacters

ModuleSourceCharacters::
  ModuleSourceCharacter ModuleSourceCharacters?

ModuleSourceCharacter::
  SourceCharacter but not one of `"` or `!` or LineTerminator

Component::
  String
  ComponentCharacters
  `[` DeclarationReference `]`

ComponentCharacters::
  ComponentCharacter ComponentCharacters?

ComponentCharacter::
  SourceCharacter but not one of `"` or Punctuator or FutureReservedPunctuator or WhiteSpace or LineTerminator

//
// Syntactic Grammar
//

// NOTE: The following grammar is incorrect as |SymbolReference| and |ModuleSource| have an
//       ambiguous parse. The correct solution is to use a cover grammar to parse
//       |SymbolReference| until we hit a `!` and then reinterpret the grammar.
DeclarationReference:
  [empty]
  SymbolReference                               // Shorthand reference to symbol
  ModuleSource `!`                              // Reference to a module
  ModuleSource `!` SymbolReference              // Reference to an export of a module
  ModuleSource `!` `~` SymbolReference          // Reference to a local of a module
  `!` SymbolReference                           // Reference to global symbol

SymbolReference:
  ComponentPath Meaning?
  Meaning

ComponentPath:
  Component
  ComponentPath `.` Component                      // Navigate via 'exports' of |ComponentPath|
  ComponentPath `#` Component                      // Navigate via 'members' of |ComponentPath|
  ComponentPath `~` Component                      // Navigate via 'locals' of |ComponentPath|

Meaning:
  `:` MeaningKeyword                            // Indicates the meaning of a symbol (i.e. ':class')
  `:` MeaningKeyword `(` DecimalDigits `)`      // Indicates an overloaded meaning (i.e. ':function(1)')
  `:` `(` DecimalDigits `)`                     // Shorthand for an overloaded meaning (i.e. `:(1)`)
  `:` DecimalDigits                             // Shorthand for an overloaded meaning (i.e. ':1')
```


</details>



</details>



```shell
```
