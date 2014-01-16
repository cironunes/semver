Versionamento Semântico 2.0.0
==============================

Sumário
-------

Dado o número de uma versão MAIOR,MENOR,PATCH, incremente o:

1. MAIOR quando você fizer mudanças que trazem incompatibilidade na API
2. MENOR quando você adicionar funcionalidade mantendo a compatibilidade com versões anteriores.
3. PATCH quando você fizer bug fixes mantendo a compatibilidade com versões anteriores.

Nomes adicionais para pre-releases e metadados de build estão disponíveis como extensões ao formato MAIOR.MENOR.PATCH.

Introdução
------------

Em um mundo de gerenciamento de software existe um lugar pavoroso chamado
“*dependency hell*”. Quanto mais seu sistema cresce e mais pacotes você
integra no seu software, mais você vai se encontrar, um dia, neste poço de
desespero.

Em sistemas com muitas dependências, lançar novas versões de pacotes podem
rapidamente se tornar um pesadelo.	Se as especificações das dependências
estiverem muito acopladas, você corre  perigo de *version lock*
(impossibilidade de atualizar um pacote sem ter que lançar uma versão nova
de cada pacote que é dependência). Se as dependências estiverem muito
desacopladas, você vai inevitavelmente ser mordido pela promiscuidade de
versão (assumindo compatibilidade com mais versões futuras do que o sensato).
*Dependency hell* é onde você está quando o *version lock* e/ou a
promiscuidade de versão não te deixam ir com o projeto adiante de forma fácil
e segura.

Como solução para este problema, eu proponho um simples conjunto de regras e
requerimentos que ditam como os números de versão são atribuídos e
incrementados. Estas regras são baseadas em, mas não necessariamente limitadas
a práticas comuns já bastante difundidas, usadas em ambos, softwares fechados
e open-source. Para este sistema funcionar, primeiro você precisa declarar uma
API pública. A declaração pode ser feita via documentação ou no próprio código.
Entretanto, é importante que a API seja limpa e precisa. Uma vez que
você identifica o público da sua API, você comunica as mudanças dela com
incrementos especificos ao seu número de versão. Considerando um formato de
versão X.Y.Z (Major.Minor.Patch). Correções de bugs que não afetam a API incrementam
o patch, adições/mudanças compativéis com as versões anteriores
incrementam o minor e mudanças na API não compatíveis com as versões anterioes
incrementam o major.

Eu chamo este sistema de "Versionamento Semântico". Neste esquema, os números de versão e a forma que eles mudam transmitem o significado do código subjacente e o que foi modificado de uma versão para a próxima.


Semantic Versioning Specification (SemVer)
------------------------------------------

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD",
"SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be
interpreted as described in [RFC 2119](http://tools.ietf.org/html/rfc2119).

1. Software using Semantic Versioning MUST declare a public API. This API
could be declared in the code itself or exist strictly in documentation.
However it is done, it should be precise and comprehensive.

1. A normal version number MUST take the form X.Y.Z where X, Y, and Z are
non-negative integers, and MUST NOT contain leading zeroes. X is the
major version, Y is the minor version, and Z is the patch version.
Each element MUST increase numerically. For instance: 1.9.0 -> 1.10.0 -> 1.11.0.

1. Once a versioned package has been released, the contents of that version
MUST NOT be modified. Any modifications MUST be released as a new version.

1. Major version zero (0.y.z) is for initial development. Anything may change
at any time. The public API should not be considered stable.

1. Version 1.0.0 defines the public API. The way in which the version number
is incremented after this release is dependent on this public API and how it
changes.

1. Patch version Z (x.y.Z | x > 0) MUST be incremented if only backwards
compatible bug fixes are introduced. A bug fix is defined as an internal
change that fixes incorrect behavior.

1. Minor version Y (x.Y.z | x > 0) MUST be incremented if new, backwards
compatible functionality is introduced to the public API. It MUST be
incremented if any public API functionality is marked as deprecated. It MAY be
incremented if substantial new functionality or improvements are introduced
within the private code. It MAY include patch level changes. Patch version
MUST be reset to 0 when minor version is incremented.

1. Major version X (X.y.z | X > 0) MUST be incremented if any backwards
incompatible changes are introduced to the public API. It MAY also include minor
and patch level changes. Patch and minor version MUST be reset to 0 when major
version is incremented.

1. A pre-release version MAY be denoted by appending a hyphen and a
series of dot separated identifiers immediately following the patch
version. Identifiers MUST comprise only ASCII alphanumerics and hyphen
[0-9A-Za-z-]. Identifiers MUST NOT be empty. Numeric identifiers MUST
NOT include leading zeroes. Pre-release versions have a lower
precedence than the associated normal version. A pre-release version
indicates that the version is unstable and might not satisfy the
intended compatibility requirements as denoted by its associated
normal version. Examples: 1.0.0-alpha, 1.0.0-alpha.1, 1.0.0-0.3.7,
1.0.0-x.7.z.92.

1. Build metadata MAY be denoted by appending a plus sign and a series of dot
separated identifiers immediately following the patch or pre-release version.
Identifiers MUST comprise only ASCII alphanumerics and hyphen [0-9A-Za-z-].
Identifiers MUST NOT be empty. Build metadata MUST be ignored when determining
version precedence. Thus two versions that differ only in the build metadata,
have the same precedence. Examples: 1.0.0-alpha+001, 1.0.0+20130313144700,
1.0.0-beta+exp.sha.5114f85.

1. Precedence refers to how versions are compared to each other when ordered.
Precedence MUST be calculated by separating the version into major, minor, patch
and pre-release identifiers in that order (Build metadata does not figure
into precedence). Precedence is determined by the first difference when
comparing each of these identifiers from left to right as follows: Major, minor,
and patch versions are always compared numerically. Example: 1.0.0 < 2.0.0 <
2.1.0 < 2.1.1. When major, minor, and patch are equal, a pre-release version has
lower precedence than a normal version. Example: 1.0.0-alpha < 1.0.0. Precedence
for two pre-release versions with the same major, minor, and patch version MUST
be determined by comparing each dot separated identifier from left to right
until a difference is found as follows: identifiers consisting of only digits
are compared numerically and identifiers with letters or hyphens are compared
lexically in ASCII sort order. Numeric identifiers always have lower precedence
than non-numeric identifiers. A larger set of pre-release fields has a higher
precedence than a smaller set, if all of the preceding identifiers are equal.
Example: 1.0.0-alpha < 1.0.0-alpha.1 < 1.0.0-alpha.beta < 1.0.0-beta <
1.0.0-beta.2 < 1.0.0-beta.11 < 1.0.0-rc.1 < 1.0.0.

Backus–Naur Form Grammar for Valid SemVer Versions
--------------------------------------------------

    <valid semver> ::= <version core>
                     | <version core> "-" <pre-release>
                     | <version core> "+" <build>
                     | <version core> "-" <pre-release> "+" <build>

    <version core> ::= <major> "." <minor> "." <patch>

    <major> ::= <numeric identifier>

    <minor> ::= <numeric identifier>

    <patch> ::= <numeric identifier>

    <pre-release> ::= <dot-separated pre-release identifiers>

    <dot-separated pre-release identifiers> ::= <pre-release identifier>
                                              | <pre-release identifier> "." <dot-separated pre-release identifiers>

    <build> ::= <dot-separated build identifiers>

    <dot-separated build identifiers> ::= <build identifier>
                                        | <build identifier> "." <dot-separated build identifiers>

    <pre-release identifier> ::= <alphanumeric identifier>
                               | <numeric identifier>

    <build identifier> ::= <alphanumeric identifier>
                         | <digits>

    <alphanumeric identifier> ::= <non-digit>
                                | <non-digit> <identifier characters>
                                | <identifier characters> <non-digit>
                                | <identifier characters> <non-digit> <identifier characters>

    <numeric identifier> ::= "0"
                           | <positive digit>
                           | <positive digit> <digits>

    <identifier characters> ::= <identifier character>
                              | <identifier character> <identifier characters>

    <identifier character> ::= <digit>
                             | <non-digit>

    <non-digit> ::= <letter>
                  | "-"

    <digits> ::= <digit>
               | <digit> <digits>

    <digit> ::= "0"
              | <positive digit>

    <positive digit> ::= "1" | "2" | "3" | "4" | "5" | "6" | "7" | "8" | "9"

    <letter> ::= "A" | "B" | "C" | "D" | "E" | "F" | "G" | "H" | "I" | "J"
               | "K" | "L" | "M" | "N" | "O" | "P" | "Q" | "R" | "S" | "T"
               | "U" | "V" | "W" | "X" | "Y" | "Z" | "a" | "b" | "c" | "d"
               | "e" | "f" | "g" | "h" | "i" | "j" | "k" | "l" | "m" | "n"
               | "o" | "p" | "q" | "r" | "s" | "t" | "u" | "v" | "w" | "x"
               | "y" | "z"


Por que usar o versionamento semântico?
---------------------------------------

Esta não é uma idéia nova ou revolucionária. Na verdade, você provavelmente
já faz algo parecido. O problema é que "parecido" não é bom o suficiente. Sem
o cumprimento de algum tipo de especificação formal, o número de versões são
praticamente inúteis para o gerenciamento de dependência. Ao dar um nome e uma
definição clara para as idéias apresentadas acima, fica mais fácil de comunicar
as suas intenções para os usuários de seu software. Uma vez que estas intenções
sejam claras, a especificação das dependências podem finalmente ser flexível
(mas  não tão flexível).

Um exemplo simples sobre o versionamento semântico pode demonstrar como aquela
frustação de gerenciamento de dependência é coisa do passado. Considere uma
biblioteca chamada "CarroDeBombeiro", a qual precisa de um pacote "Escada"
versionado semanticamente. No momento em que é criado o CarroDeBombeiro, o
pacote Escada está na versão 3.1.0. Um vez que CarroDeBombeiro utilize
funcionalidades introduzidas em 3.1.0, você pode especificar a versão de Escada
como maior ou igual a 3.1.0, e menor que 4.0.0 com uma certa segurança. Assim
que a versão 3.1.1 e 3.2.0 de Escada estiver disponível, você pode usá-la no
seu sistema de gerenciamento de pacotes e certificar que essas versões serão
compatíveis com o software existente.

Como um desenvolvedor responsável, é claro que você vai querer verificar se
todas as atualizações de pacotes funcionam como anunciado. O mundo real não é
um lugar tão confiável, infelizmente não há nada que possamos fazer sobre isso,
mas podemos pelo menos ser atentos. O que você pode fazer é deixar o
Versionamento Semântico fornecer um caminho sensato para atualizar e lançar
novos pacotes, sem ter que se enrolar em versões recentes, economizando tempo
e evitando aborrecimentos.

Se tudo isso lhe parece conveniente, tudo que você precisa fazer para começar a
usar o Versionamento Semântico é avisar que você está seguindo e respeitando as
regras. Faça um link para esse site no README de seu projeto para que as outras
pessoas saibam dessas regras e possam se beneficiar delas.

FAQ
---

### How should I deal with revisions in the 0.y.z initial development phase?

The simplest thing to do is start your initial development release at 0.1.0
and then increment the minor version for each subsequent release.

### How do I know when to release 1.0.0?

If your software is being used in production, it should probably already be
1.0.0. If you have a stable API on which users have come to depend, you should
be 1.0.0. If you're worrying a lot about backwards compatibility, you should
probably already be 1.0.0.

### Doesn't this discourage rapid development and fast iteration?

Major version zero is all about rapid development. If you're changing the API
every day you should either still be in version 0.y.z or on a separate
development branch working on the next major version.

### If even the tiniest backwards incompatible changes to the public API require a major version bump, won't I end up at version 42.0.0 very rapidly?

This is a question of responsible development and foresight. Incompatible
changes should not be introduced lightly to software that has a lot of
dependent code. The cost that must be incurred to upgrade can be significant.
Having to bump major versions to release incompatible changes means you'll
think through the impact of your changes, and evaluate the cost/benefit ratio
involved.

### Documenting the entire public API is too much work!

It is your responsibility as a professional developer to properly document
software that is intended for use by others. Managing software complexity is a
hugely important part of keeping a project efficient, and that's hard to do if
nobody knows how to use your software, or what methods are safe to call. In
the long run, Semantic Versioning, and the insistence on a well defined public
API can keep everyone and everything running smoothly.

### What do I do if I accidentally release a backwards incompatible change as a minor version?

As soon as you realize that you've broken the Semantic Versioning spec, fix
the problem and release a new minor version that corrects the problem and
restores backwards compatibility. Even under this circumstance, it is
unacceptable to modify versioned releases. If it's appropriate,
document the offending version and inform your users of the problem so that
they are aware of the offending version.

### What should I do if I update my own dependencies without changing the public API?

That would be considered compatible since it does not affect the public API.
Software that explicitly depends on the same dependencies as your package
should have their own dependency specifications and the author will notice any
conflicts. Determining whether the change is a patch level or minor level
modification depends on whether you updated your dependencies in order to fix
a bug or introduce new functionality. I would usually expect additional code
for the latter instance, in which case it's obviously a minor level increment.

### What if I inadvertently alter the public API in a way that is not compliant with the version number change (i.e. the code incorrectly introduces a major breaking change in a patch release)

Use your best judgment. If you have a huge audience that will be drastically
impacted by changing the behavior back to what the public API intended, then
it may be best to perform a major version release, even though the fix could
strictly be considered a patch release. Remember, Semantic Versioning is all
about conveying meaning by how the version number changes. If these changes
are important to your users, use the version number to inform them.

### How should I handle deprecating functionality?

Deprecating existing functionality is a normal part of software development and
is often required to make forward progress. When you deprecate part of your
public API, you should do two things: (1) update your documentation to let
users know about the change, (2) issue a new minor release with the deprecation
in place. Before you completely remove the functionality in a new major release
there should be at least one minor release that contains the deprecation so
that users can smoothly transition to the new API.

### Does SemVer have a size limit on the version string?

No, but use good judgment. A 255 character version string is probably overkill,
for example. Also, specific systems may impose their own limits on the size of
the string.

About
-----

The Semantic Versioning specification is authored by [Tom
Preston-Werner](http://tom.preston-werner.com), inventor of Gravatars and
cofounder of GitHub.

If you'd like to leave feedback, please [open an issue on
GitHub](https://github.com/mojombo/semver/issues).


License
-------

Creative Commons - CC BY 3.0
http://creativecommons.org/licenses/by/3.0/
