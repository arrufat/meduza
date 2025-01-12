## :lizard: :mermaid: **meduza**

[![CI][ci-shield]][ci-url]
[![CD][cd-shield]][cd-url]
[![Meduza][mdz-shield]][mdz-url]
[![License][license-shield]][license-url]

### Zig codebase graph generator that emits a [Mermaid class diagram](https://mermaid.js.org/syntax/classDiagram.html).

#### :rocket: Usage

```sh
git clone https://github.com/tensorush/meduza
cd meduza/
zig build exe -- -h
```

#### :sparkles: Features

- Generate either `.html`, `.md`, or `.mmd` Mermaid class diagram.

- Generate one diagram for each of your codebase's source directories.

- Learn how to improve code readability from logged tips (enable with `-i`).

- Convert `.md` or `.mmd` diagram to `.svg` with Mermaid CLI ([see CD pipeline](https://github.com/tensorush/meduza/blob/main/.github/workflows/cd.yaml#L48)).

- Generate a large diagram (`maxTextSize` > 50'000) with Mermaid CLI ([see CD pipeline](https://github.com/tensorush/meduza/blob/main/.github/workflows/cd.yaml#L47)).

- Click on types to go to respective code lines on the remote (GitHub Mermaid forbids this, though).

#### :world_map: Legend

```mermaid
---
title: Title (path/to/directory)
---
%%{
    init: {
        'theme': 'base',
        'themeVariables': {
            'fontSize': '18px',
            'fontFamily': 'arial',
            'lineColor': '#F6A516',
            'primaryColor': '#28282B',
            'primaryTextColor': '#F6A516'
        }
    }
}%%
classDiagram
class `file.zig` {
    fld: T
    test "tst"()
}
class Error["Error [err]"] {
    Value
}
class Enum["Enum [enu]"] {
    Value
    +func(arg) E!R
}
class Union["Union [uni]"] {
    fld: T
    +func(arg) E!R
}
class Struct["Struct [str]"] {
    fld: T
    +func(arg) E!R
}
class Opaque["Opaque [opa]"] {
    fld: T
    +func(arg) E!R
}
`file.zig` <-- Error
`file.zig` <-- Enum
`file.zig` <-- Union
`file.zig` <-- Struct
`file.zig` <-- Opaque
```

| Type          |                  Zig                  |                  Meduza                   |
|---------------|:-------------------------------------:|:-----------------------------------------:|
| File          |              `file.zig`               |            `class file.zig {}`            |
| Error         |   `const Error = error { Value, };`   |  `class Error["Error [err]"] { Value }`   |
| Enum          |    `const Enum = enum { Value, };`    |   `class Enum["Enum [enu]"] { Value }`    |
| Union         |  `const Union = union { fld: T, };`   |  `class Union["Union [uni]"] { fld: T }`  |
| Struct        | `const Struct = struct { fld: T, };`  | `class Struct["Struct [str]"] { fld: T }` |
| Opaque        | `const Opaque = opaque { fld: T, };`  | `class Opaque["Opaque [opa]"] { fld: T }` |
| Function      |  `pub fn` / `fn` `func(arg) E!R {}`   |        `+` / `-` `func(arg) : E!R`        |
| Error union   |   `error{Value}!struct { fld: T }`    |     `error[Value]!struct [ fld: T ]`      |
| Test function |            `test "tst" {}`            |              `test "tst"()`               |
| Type relation | `B.zig`: `const A = enum { Value, };` |               `B.zig <-- A`               |

<!-- MARKDOWN LINKS -->

[ci-shield]: https://img.shields.io/github/actions/workflow/status/tensorush/meduza/ci.yaml?branch=main&style=for-the-badge&logo=github&label=CI&labelColor=black
[ci-url]: https://github.com/tensorush/meduza/blob/main/.github/workflows/ci.yaml
[cd-shield]: https://img.shields.io/github/actions/workflow/status/tensorush/meduza/cd.yaml?branch=main&style=for-the-badge&logo=github&label=CD&labelColor=black
[cd-url]: https://github.com/tensorush/meduza/blob/main/.github/workflows/cd.yaml
[mdz-shield]: https://img.shields.io/badge/click-F6A516?style=for-the-badge&logo=zig&logoColor=F6A516&label=meduza&labelColor=black
[mdz-url]: https://tensorush.github.io/meduza/src.svg
[license-shield]: https://img.shields.io/github/license/tensorush/meduza.svg?style=for-the-badge&labelColor=black&kill_cache=1
[license-url]: https://github.com/tensorush/meduza/blob/main/LICENSE.md
