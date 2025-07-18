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























<br><br>

---

<br><br>



# Tags

<details><summary>Click to expand..</summary>

### **Teil 1: Das Fundament – TSDoc Kernkonzepte**

Dieser Abschnitt definiert die grundlegenden Bausteine und Regeln des TSDoc-Systems.

#### **1.1 Die drei Tag-Kategorien**

Jeder Tag in TSDoc gehört zu genau einer dieser drei Kategorien, die seine syntaktische Rolle bestimmen.

| Kategorie | Erkennungsmerkmal | Zweck & Verhalten |
| :--- | :--- | :--- |
| **Block Tag** | `@tagname` am Zeilenanfang. | Definiert einen eigenständigen, thematischen Inhaltsblock. Der gesamte Text bis zum nächsten Tag gehört zu diesem Block. |
| **Modifier Tag**| `@tagname` am Zeilenanfang, meist ohne nachfolgenden Inhalt. | Weist einem API-Element eine spezifische Eigenschaft oder ein Metadatum zu (z.B. Sichtbarkeit, Status). |
| **Inline Tag** | `{` `@tagname ...` `}` direkt im Textfluss. | Wird innerhalb von Textblöcken verwendet, um dynamische Inhalte wie Hyperlinks oder geerbte Dokumentation einzufügen. |

#### **1.2 Die drei Standardisierungs-Gruppen**

Diese Gruppen klassifizieren die Verbindlichkeit und den Support-Level eines Tags über verschiedene TSDoc-kompatible Tools hinweg.

| Gruppe | Verbindlichkeit | Bedeutung für die Praxis |
| :--- | :--- | :--- |
| **Core** | **Essenziell & verpflichtend.** | Jedes TSDoc-Tool muss diese Tags und ihre Semantik vollständig unterstützen. Absolut verlässlich. |
| **Extended** | **Optional, aber standardisiert.** | Tools können diese Tags unterstützen. Wenn sie es tun, müssen sie sich an die offizielle Syntax und Semantik halten. |
| **Discretionary**| **Optional & implementierungsspezifisch.** | Syntax ist meist vorgegeben, die genaue Bedeutung kann sich aber je nach Tool unterscheiden. Für spezielle Anwendungsfälle. |

#### **1.3 Die Deklarations-Referenz-Syntax**

Dies ist die Grammatik zur eindeutigen Adressierung von Code-Elementen, die hauptsächlich in `@link` und `@inheritDoc` Tags verwendet wird.

*   **Grundlagen:** Eine Referenz kann auf globale Symbole, Module oder deren Exporte und Member verweisen.
*   **Navigations-Operatoren:**
    *   `!` : Trennt eine Modulquelle vom Symbol (`ModuleSource!SymbolReference`). Dient als Einstiegspunkt in ein Paket.
    *   `.` : Navigiert zu `exports` eines Symbols.
    *   `#` : Navigiert zu `members` (Instanz-Member) eines Symbols.
    *   `~` : Navigiert zu `locals` (interne, nicht-exportierte Member) eines Symbols.
*   **Syntax-Muster:**
    *   **Globales Symbol:** `!MyGlobal`
    *   **Modul-Referenz:** `my-package-name!`
    *   **Export eines Moduls:** `my-package-name!MyClass`
    *   **Member einer Klasse:** `MyClass#myMethod`
    *   **Bedeutung/Disambiguierung:** Ein Doppelpunkt `:` gefolgt von einem Schlüsselwort (`:class`, `:function(1)`) löst Mehrdeutigkeiten auf.

---

### **Teil 2: Das TSDoc Tag-Verzeichnis**

Eine vollständige, alphabetisch geordnete Referenz aller Standard-Tags. Jeder Eintrag folgt einem identischen, maschinenlesbaren Schema.

---

### `@alpha`

| Eigenschaft | Wert |
| :--- | :--- |
| **Syntax** | Modifier Tag |
| **Standard** | Discretionary |

**Zweck & Anwendung:**
Markiert ein API-Element als im "Alpha"-Stadium. Es ist für die Nutzung durch Dritte vorgesehen, aber noch nicht final freigegeben und kann sich jederzeit ohne Vorwarnung ändern. Tooling kann dieses Element aus einem Public Release entfernen.

**Beispiel:**
```typescript
/**
 * Represents a book in the catalog.
 * @public
 */
export class Book {
  /**
   * The title of the book.
   * @alpha
   */
  public get title(): string;

  /**
   * The author of the book.
   */
  public get author(): string;
}
```

---

### `@beta`

| Eigenschaft | Wert |
| :--- | :--- |
| **Syntax** | Modifier Tag |
| **Standard** | Discretionary |
| **Synonyme** | `@experimental` |

**Zweck & Anwendung:**
Markiert ein API-Element als im "Beta"-Stadium. Es wurde experimentell für Dritte freigegeben, um Feedback zu sammeln. Es sollte nicht in Produktionsumgebungen verwendet werden, da sich der Vertrag ändern kann.

**Beispiel:**
```typescript
/**
 * Represents a book in the catalog.
 * @public
 */
export class Book {
  /**
   * The title of the book.
   * @beta
   */
  public get title(): string;

  /**
   * The author of the book.
   */
  public get author(): string;
}
```

---

### `@decorator`

| Eigenschaft | Wert |
| :--- | :--- |
| **Syntax** | Block Tag |
| **Standard** | Extended |

**Zweck & Anwendung:**
Dient als Workaround, um ECMAScript-Decorators zu dokumentieren, da diese vom TypeScript-Compiler nicht in die `.d.ts`-Ausgabedateien übernommen werden. Der Decorator-Ausdruck wird als Text zitiert.

**Beispiel:**
```typescript
class Book {
  /**
   * The title of the book.
   * @decorator `@jsonSerialized`
   * @decorator `@jsonFormat(JsonFormats.Url)`
   */
  @jsonSerialized
  @jsonFormat(JsonFormats.Url)
  public website: string;
}
```

---

### `@deprecated`

| Eigenschaft | Wert |
| :--- | :--- |
| **Syntax** | Block Tag |
| **Standard** | Core |

**Zweck & Anwendung:**
Kommuniziert, dass ein API-Element nicht mehr unterstützt wird und in einer zukünftigen Version entfernt werden kann. Dem Tag sollte ein Satz folgen, der die empfohlene Alternative beschreibt. Gilt rekursiv für alle untergeordneten Member.

**Beispiel:**
```typescript
/**
 * The base class for controls that can be rendered.
 *
 * @deprecated Use the new {@link Control} base class instead.
 */
export class VisualControl {
  // . . .
}
```

---

### `@defaultValue`

| Eigenschaft | Wert |
| :--- | :--- |
| **Syntax** | Block Tag |
| **Standard** | Extended |

**Zweck & Anwendung:**
Dokumentiert den Standardwert für ein Feld oder eine Eigenschaft, wenn kein expliziter Wert zugewiesen wird.

**Beispiel:**
```typescript
interface IWarningOptions {
  /**
   * Determines how the warning will be displayed.
   * @defaultValue `WarningStyle.DialogBox`
   */
  warningStyle?: WarningStyle;
}
```

---

### `@eventProperty`

| Eigenschaft | Wert |
| :--- | :--- |
| **Syntax** | Modifier Tag |
| **Standard** | Extended |

**Zweck & Anwendung:**
Zeigt bei einer Klassen- oder Interface-Eigenschaft an, dass diese ein Event-Objekt zurückgibt, an das Event-Handler angehängt werden können. Dokumentations-Tools können solche Eigenschaften unter einer eigenen "Events"-Überschrift anzeigen.

**Beispiel:**
```typescript
class MyClass {
  /**
   * This event is fired whenever the application navigates to a new page.
   * @eventProperty
   */
  public readonly navigatedEvent: FrameworkEvent<NavigatedEventArgs>;
}
```

---

### `@example`

| Eigenschaft | Wert |
| :--- | :--- |
| **Syntax** | Block Tag |
| **Standard** | Extended |

**Zweck & Anwendung:**
Leitet einen Abschnitt ein, der ein Anwendungsbeispiel für die API illustriert. Text auf derselben Zeile wie `@example` wird als Titel für das Beispiel interpretiert.

**Beispiel:**
```typescript
/**
 * Adds two numbers together.
 * @example
 * Here's a simple example:
 * ```
 * // Prints "2":
 * console.log(add(1,1));
 * ```
 * @example Here's an example with negative numbers:
 * ```
 * // Prints "0":
 * console.log(add(1,-1));
 * ```
 */
export function add(x: number, y: number): number {}
```

---

### `@experimental`

| Eigenschaft | Wert |
| :--- | :--- |
| **Syntax** | Modifier Tag |
| **Standard** | Discretionary |
| **Synonyme** | `@beta` |

**Zweck & Anwendung:**
Identische Semantik wie `@beta`. Wird von Tools verwendet, die keine separate `@alpha`-Phase unterstützen.

**Beispiel:**
```typescript
/**
 * Represents a book in the catalog.
 * @public
 */
export class Book {
  /**
   * The title of the book.
   * @experimental
   */
  public get title(): string;
}
```

---

### `@inheritDoc`

| Eigenschaft | Wert |
| :--- | :--- |
| **Syntax** | Inline Tag |
| **Standard** | Extended |

**Zweck & Anwendung:**
Kopiert die Dokumentation (Zusammenfassung, `@remarks`, `@params`, `@typeParam`, `@returns`) von einem anderen API-Element. Andere Tags wie `@example` werden nicht kopiert.

**Beispiel:**
```typescript
export class Button implements IWidget {
  /** {@inheritDoc IWidget.draw} */
  public draw(x: number, y: number): void {
    // . . .
  }
}
```

---

### `@internal`

| Eigenschaft | Wert |
| :--- | :--- |
| **Syntax** | Modifier Tag |
| **Standard** | Discretionary |

**Zweck & Anwendung:**
Markiert ein API-Element als nicht für die Nutzung durch Dritte vorgesehen. Tooling kann dieses Element aus einer öffentlichen Dokumentation oder Release-Artefakten entfernen.

**Beispiel:**
```typescript
/**
 * Represents a book in the catalog.
 * @public
 */
export class Book {
  /**
   * The title of the book.
   * @internal
   */
  public get _title(): string;
}
```

---

### `@label`

| Eigenschaft | Wert |
| :--- | :--- |
| **Syntax** | Inline Tag |
| **Standard** | Core |

**Zweck & Anwendung:**
Vergibt ein eindeutiges Label für eine Deklaration (z.B. einen Indexer oder eine Funktionsüberladung), um sie über die Deklarations-Referenz-Syntax eindeutig referenzierbar zu machen.

**Beispiel:**
```typescript
export interface Interface {
  /**
   * {@label STRING_INDEXER}
   */
  [key: string]: number;
}
```

---

### `@link`

| Eigenschaft | Wert |
| :--- | :--- |
| **Syntax** | Inline Tag |
| **Standard** | Core |

**Zweck & Anwendung:**
Erstellt Hyperlinks zu externen URLs oder anderen API-Elementen mittels Deklarations-Referenz-Syntax. Optional kann ein alternativer Link-Text angegeben werden.

**Beispiel:**
```typescript
/**
 * Links can point to a URL: {@link https://github.com/microsoft/tsdoc}
 *
 * Links can point to an API item: {@link Button}
 *
 * You can optionally include custom link text: {@link Button | the Button class}
 *
 * It can also reference a member of a class:
 * {@link controls.Button.render | the render() method}
 */
```

---

### `@override`

| Eigenschaft | Wert |
| :--- | :--- |
| **Syntax** | Modifier Tag |
| **Standard** | Extended |

**Zweck & Anwendung:**
Zeigt explizit an, dass eine Methode oder Eigenschaft eine Definition aus einer Basisklasse überschreibt. Gegenstück zu `@virtual`.

**Beispiel:**
```typescript
class Base {
  /** @virtual */
  public render(): void {}
}

class Child extends Base {
  /** @override */
  public render(): void;
}
```

---

### `@packageDocumentation`

| Eigenschaft | Wert |
| :--- | :--- |
| **Syntax** | Modifier Tag |
| **Standard** | Core |

**Zweck & Anwendung:**
Markiert, dass ein Kommentarblock ein gesamtes NPM-Paket beschreibt. Dieser Kommentar muss der erste `/** ... */`-Block in der Entrypoint-Datei des Pakets sein und darf nicht für ein einzelnes API-Element verwendet werden.

**Beispiel:**
```typescript
/**
 * A library for building widgets.
 *
 * @remarks
 * The `widget-lib` defines the {@link IWidget} interface...
 *
 * @packageDocumentation
 */
```

---

### `@param`

| Eigenschaft | Wert |
| :--- | :--- |
| **Syntax** | Block Tag |
| **Standard** | Core |

**Zweck & Anwendung:**
Dokumentiert einen Parameter einer Funktion. Die Syntax ist `@param parameterName - Beschreibung`.

**Beispiel:**
```typescript
/**
 * Returns the average of two numbers.
 * @param x - The first input number
 * @param y - The second input number
 * @returns The arithmetic mean of `x` and `y`
 */
function getAverage(x: number, y: number): number {
  return (x + y) / 2.0;
}
```

---

### `@privateRemarks`

| Eigenschaft | Wert |
| :--- | :--- |
| **Syntax** | Block Tag |
| **Standard** | Core |

**Zweck & Anwendung:**
Startet einen Inhaltsblock, der nicht für die öffentliche Zielgruppe bestimmt ist. Ein TSDoc-Tool muss diesen gesamten Abschnitt aus allen öffentlichen Ausgaben (Websites, `.d.ts`-Dateien) entfernen.

**Beispiel:**
```typescript
/**
 * Summary for the public.
 * @remarks
 * Remarks for the public.
 * @privateRemarks
 * This content is for internal developers only and will be stripped
 * from public documentation.
 */
```

---

### `@public`

| Eigenschaft | Wert |
| :--- | :--- |
| **Syntax** | Modifier Tag |
| **Standard** | Discretionary |

**Zweck & Anwendung:**
Markiert ein API-Element als offiziell freigegeben ("public"). Seine Signatur wird als stabil garantiert (z.B. gemäß Semantic Versioning).

**Beispiel:**
```typescript
/**
 * Represents a book in the catalog.
 * @public
 */
export class Book {
  /**
   * The author of the book.
   */
  public get author(): string;
}
```

---

### `@readonly`

| Eigenschaft | Wert |
| :--- | :--- |
| **Syntax** | Modifier Tag |
| **Standard** | Extended |

**Zweck & Anwendung:**
Markiert ein API-Element als schreibgeschützt, auch wenn die Typsystem-Implementierung (z.B. ein Setter, der immer einen Fehler wirft) etwas anderes nahelegt.

**Beispiel:**
```typescript
export class Book {
  /**
   * @readonly
   */
  public get title(): string {
    return this._title;
  }

  public set title(value: string) {
    throw new Error('This property is read-only!');
  }
}
```

---

### `@remarks`

| Eigenschaft | Wert |
| :--- | :--- |
| **Syntax** | Block Tag |
| **Standard** | Core |

**Zweck & Anwendung:**
Trennt die kurze Zusammenfassung (Summary) von der ausführlichen Beschreibung eines API-Elements. Der Inhalt nach `@remarks` bildet den Hauptteil der Detaildokumentation.

**Beispiel:**
```typescript
/**
 * The summary section should be brief.
 *
 * @remarks
 * The main documentation for an API item is separated into a brief
 * "summary" section optionally followed by an `@remarks` block containing
 * additional details.
 */
```

---

### `@returns`

| Eigenschaft | Wert |
| :--- | :--- |
| **Syntax** | Block Tag |
| **Standard** | Core |

**Zweck & Anwendung:**
Dokumentiert den Rückgabewert einer Funktion.

**Beispiel:**
```typescript
/**
 * Returns the average of two numbers.
 * @param x - The first input number.
 * @param y - The second input number.
 * @returns The arithmetic mean of `x` and `y`.
 */
function getAverage(x: number, y: number): number {
  return (x + y) / 2.0;
}
```

---

### `@sealed`

| Eigenschaft | Wert |
| :--- | :--- |
| **Syntax** | Modifier Tag |
| **Standard** | Extended |

**Zweck & Anwendung:**
Verhindert, dass von einer Klasse geerbt wird oder dass eine Methode/Eigenschaft in einer Unterklasse überschrieben wird. Gegenstück zu `@virtual`.

**Beispiel:**
```typescript
class Base {
  /** @virtual */
  public render(): void {}

  /** @sealed */
  public initialize(): void {}
}
```

---

### `@see`

| Eigenschaft | Wert |
| :--- | :--- |
| **Syntax** | Block Tag |
| **Standard** | Extended |

**Zweck & Anwendung:**
Erstellt eine "Siehe auch"-Liste mit Verweisen auf andere API-Elemente oder Ressourcen. Jeder `@see`-Block wird zu einem separaten Punkt in der Liste. Hyperlinks müssen explizit mit `{@link}` erstellt werden.

**Beispiel:**
```typescript
/**
 * Parses a string containing a Uniform Resource Locator (URL).
 * @see {@link ParsedUrl} for the returned data structure.
 * @see {@link https://tools.ietf.org/html/rfc1738|RFC 1738} for syntax.
 */
function parseURL(url: string): ParsedUrl;
```

---

### `@throws`

| Eigenschaft | Wert |
| :--- | :--- |
| **Syntax** | Block Tag |
| **Standard** | Extended |

**Zweck & Anwendung:**
Dokumentiert einen Exception-Typ, der von einer Funktion geworfen werden kann. Für jeden Exception-Typ sollte ein eigener `@throws`-Block verwendet werden.

**Beispiel:**
```typescript
/**
 * @throws {@link IsbnSyntaxError}
 * This exception is thrown if the input is not a valid ISBN number.
 *
 * @throws {@link book-lib#BookNotFoundError}
 * Thrown if the ISBN number is valid, but no such book exists.
 */
function fetchBookByIsbn(isbnCode: string): Book;
```

---

### `@typeParam`

| Eigenschaft | Wert |
| :--- | :--- |
| **Syntax** | Block Tag |
| **Standard** | Core |
| **Synonyme** | `<T>` (in JSDoc/JavaDoc) |

**Zweck & Anwendung:**
Dokumentiert einen generischen Typparameter (z.B. `<T>`). Die Syntax ist `@typeParam T - Beschreibung`.

**Beispiel:**
```typescript
/**
 * Wrapper for an HTTP Response.
 * @typeParam B - Response body
 * @typeParam H - Headers
 */
interface HttpResponse<B, H> {
  body: B;
  headers: H;
}
```

---

### `@virtual`

| Eigenschaft | Wert |
| :--- | :--- |
| **Syntax** | Modifier Tag |
| **Standard** | Extended |

**Zweck & Anwendung:**
Zeigt explizit an, dass eine Methode oder Eigenschaft von Unterklassen überschrieben werden darf. Gegenstück zu `@sealed` und `@override`.

**Beispiel:**
```typescript
class Base {
  /** @virtual */
  public render(): void {}
}

class Child extends Base {
  /** @override */
  public render(): void;
}
```

</details>




