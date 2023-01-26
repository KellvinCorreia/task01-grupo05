## O que é o git rebase?

Rebasing é o processo de mover ou combinar uma sequência de commits para um novo commit base. O rebasing é mais útil e melhor visualizado no contexto do fluxo de trabalho de ramificação de recurso. O processo geral pode ser visualizado da seguinte forma:

![Tutorial Git: Git rebase](https://wac-cdn.atlassian.com/dam/jcr:4e576671-1b7f-43db-afb5-cf8db8df8e4a/01%20What%20is%20git%20rebase.svg?cdnVersion=742)

Normalmente, você usará `git rebase` para:

- Editar mensagens anteriores do commit
- Combinar vários commits em um
- Excluir ou reverter commits que não são mais necessários

O comando `git rebase` permite alterar com facilidade uma variedade de commits, modificando o histórico do seu repositório. É possível reordenar, editar ou combinar commits por squash.

## Sintaxe

`git rebase <nome-da-branch>`

### Outros comandos

`pick`

`pick` significa simplesmente que o commit está incluído. A reorganização da ordem dos comandos `pick` altera a ordem dos commits quando a troca de base está em andamento. Se você optar por não incluir um commit, será preciso excluir a linha toda.

`reword`

O comando `reword` é semelhante a `pick`, mas depois que você usá-lo, o processo de troca de base será colocado em pausa e dará a você a chance de alterar a mensagem de commit. As alterações feitas pelo commit não são afetadas.

`edit`

Se você optar por `edit` um commit, terá a chance de alterar o commit, o que significa que pode adicionar ou alterar o commit por completo. Também é possível fazer mais commits antes de continuar com o rebase. Isso permite que você divida um commit grande em commits menores ou remova alterações equivocadas feitas em um commit.

`squash`

Esse comando permite combinar dois ou mais commits em um único commit. Um commit é combinado por squash no commit acima dele. O Git permite que você grave uma nova mensagem do commit descrevendo ambas as alterações.

`fixup`

Isso é semelhante a `squash`, mas o commit a ser mesclado tem a mensagem descartada. O commit simplesmente sofre merge no commit acima dele, e a mensagem do commit anterior é usado para descrever ambas as alterações.

`exec`

Permite que você execute comandos de shell arbitrários em um commit.

## Exemplo

> Branch master com 3 commits (A, B e C).

```yaml
A<---B<---C
|
|
|Master|
|
HEAD
```

Comando:

```undefined
git checkout master

```

> Após fazer o commit C, criei um novo branch com o nome design.

```yaml
HEAD
|
|design|
|
|
A<---B<---C
|
|
|Master|
```

Comando:

```bash
git commit -m "Commit C"
git checkout -b design      # cria a branch design a partir da branch atual (master)

```

> Fiz um commit (D) no branch design

```haskell
                  HEAD
                    |
                |design|
                    |
                    |
                .---D
               /
A<---B<---C<--´
          |
          |
       |Master|

```

Comando:

```bash
git checkout design
git commit -m "Commit D"

```

> e voltei ao branch master.

```yaml
                |design|
                    |
                    |
                .---D
               /
A<---B<---C<--´
          |
          |
       |Master|
          |
         HEAD

```

Comando:

```undefined
git checkout master

```

> Fiz um commit (E) no branch master.

```yaml
                |design|
                    |
                    |
                .---D
               /
A<---B<---C<--´-----E
                    |
                    |
                |Master|
                    |
                   HEAD

```

Comando:

```sql
git commit -m "Commit E"

```

E fazendo o `rebase`:

```haskell
                |design|
                    |
                    |
                .---D<----E'
               /          |
A<---B<---C<--´           |
                       |Master|

```

Comando:

```undefined
git checkout design
git rebase master

```

Como pode notar, com o `rebase` da master na branch `design`, os commits a mais (`E`) da `master` vão para o topo da branch `design`.

Assim, como pode notar ao final, os commits ficaram como você disse:

- master: A, B, C, D, E
- design: A, B, C, D

#### Referências

https://docs.github.com/pt/get-started/using-git/about-git-rebase
https://git-scm.com/docs/git-rebase
https://www.freecodecamp.org/portuguese/news/o-guia-definitivo-para-git-merge-e-git-rebase/
https://blog.betrybe.com/git/git-rebase/#1
https://www.atlassian.com/br/git/tutorials/rewriting-history/git-rebase
https://pt.stackoverflow.com/questions/81221/como-funciona-o-comando-git-rebase
