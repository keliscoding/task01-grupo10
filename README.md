# Documentação de Git

## Sumário

- [Git Rebase](#git-rebase)
- [Git Cherry Pick](#git-cherry-pick)
- [Git Revert](#git-revert)
- [Git Squash](#git-squash)

## Git Rebase
### O que é o Git Rebase?
Rebase é uma das formas que o Git possui para integrar alterações de uma ramificação para outra.
Rebasing é o processo de modificação ou de combinação uma série de commits para um novo commit base.
Um forte motivo para usá-lo é manter o projeto com um histórico linear.
### pode ser visualizado da seguinte forma:
<p align="center"><img src="https://wac-cdn.atlassian.com/dam/jcr:4e576671-1b7f-43db-afb5-cf8db8df8e4a/01%20What%20is%20git%20rebase.svg?cdnVersion=736" width="200"/></p>
Em outras palavras, o rebase literalmente altera a base do ramo do commit para outra, de forma que pareça ser criado a partir de um commit diferente.

## Uso:
Considere que você está produzindo uma feature, e a branch principal do projeto progrediu após isso. Voce pretende inserir as modificações na sua ramificação e também quer que o histórico fique limpo.

  ```git rebase branch-base```
   (branch-base indica a branch que deseja usar como base para o rebase).

## Rebase interativo
Git rebase interactive é quando o git rebase aceita um argumento --i. O "i" representa "Interactive." Sem nenhum argumento, o comando é executado no modo padrão

```git rebase --interactive <base>```
(Com o hash do commit em mãos)
Executar o git rebase com a bandeira -i dá início a uma sessão de rebasing interativa. Em vez de mover todos os commits para a nova base sem conhecimento, o rebasing interativo oferece a oportunidade de alterar os commits individuais no processo.

```
Comandos:
 p, pick = usa o commit
 r, reword = usa o commit, mas edita sua mensagem
 e, edit = usa o commit, mas para de emendar
 s, squash = usa o commit, mas mescla no commit anterior
 f, fixup = como o  "squash", mas descarta o log do commit
 x, exec = executa o comando (o resto da linha) usando o shell
 d, drop = remove o commmit
```

## Git Cherry Pick

<p align="center"><img src="https://wac-cdn.atlassian.com/dam/jcr:dff99252-7ef3-446e-88c3-7a5938d05274/git%20cherry%20pick%20illo.png?cdnVersion=725" width="200"/></p>

### Sobre

O Cherry Pick serve para pegar um commit específico feito por outro usuário e copiá-lo para a tarefa que o usuário está trabalhando. Ele consegue pegar um commit e o copia de uma branch para outra.

Caso o usuário dê um merge em um código que ainda não foi finalizado, pode ocorrer dele trazer pedaços do código que não precisa. E essas partes de código podem conter erros ou ainda nem terem sido testados. Por essa razão, essa ferramenta é tão importante para muitos cenários.

**O objetivo do Git cherry-pick é pegar um commit específico para a task em que se está trabalhando no momento sem o risco de selecionar ramificações que não são necessárias e que possam vir a causar bugs.**

Para utilizar o Cherry Pick, usa-se o seguinte comando:

```
    git cherry-pick <ID-do-Commit>
```

### Intervalo de Commits

É também possível pegar um intervalo de commits. O cherry pick permite que você informe o ID do commit inicial e o ID commit final, aqui chamado de A e B, respectivamente.

Então, quando falamos de intervalo, você tem duas opções:

Copiar todos os commits, inclusive o primeiro

```
git cherry-pick A^..B
```

Ou ignorar o primeiro commit:

```
git cherry-pick A..B
```

**É importante salientar que o commit A precisa estar após o commit B, ou seja, ser mais velho na timeline.**

### Conflitos

Assim como em merges e rebase, em cherry pick também podem acontecer conflitos, e você irá resolve-los da mesma forma que um merge/rebase.

Você pode resolve-los usando uma interface gráfica, ou via terminal.

Pelo terminal, temos dois comandos: o continue que é para você executar depois que resolver o conflito no código.

```
git cherry-pick --continue

```

E temos o abort, para cancelar o cherry pick.

```
git cherry-pick --abort
```

### Parâmetros

Esses são os comandos mais comuns que podem te ajudar:

- **-e:** permite que você edite a mensagem do commit.

- **-x:** adiciona uma mensagem no commit copiado avisando que ele é um cherry pick de um outro commit – “cherry picked from commit”.

- **–allow-empty:** por padrão, o cherry-pick não permite commits em branco, com esse parâmetro, ele sobrescreve esse comportamento.

- **–allow-empty-message:** quando o commit não tem um título, ele é barrado. Assim como no exemplo anterior, esse parâmetro sobrescreve o comportamento.

### Aviso

O Git cherry-pick é um comando muito útil quando bem utilizado, porém ele não pode substituir o git merge e o git rebase. Cada um possui uma situação que se encaixa melhor, mas isso é assunto para um próximo artigo.

Use o cherry-pick só em último caso, cuidado para não sair duplicando commits na sua linha do tempo, use com moderação!

## Git Revert

### Funcionalidade

A partir de um commit específico esse comando desfaz as alterações realizadas pelo commit informado, entretanto ele não remove o commit do histórico do projeto

### Sintaxe

Para utilizar o comando:

```
git revert "chave do commit"
```

### Aplicação do comando

Log dos commits realizados no projeto até o momento:

<p align="center"><img src="https://res.cloudinary.com/practicaldev/image/fetch/s--AFPzg9KH--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/uploads/articles/hmjgx0izetq8r3vdo7ri.png" width="400"/></p>

Arquivo html:

<p align="center"><img src="https://res.cloudinary.com/practicaldev/image/fetch/s--kH8QVbEB--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://thepracticaldev.s3.amazonaws.com/i/juutdltmncdbe59lolki.png" width="400"/></p>

Para reverter o código para situação anterior à adição de metadados deve-se utilizar o comando:

```
git revert c2f6c649
```

Obs: "c2f6c649" É a chave específica do commit que deseja reverter

##### Utilização do HEAD no revert

Uma outra forma de utilizar **git revert** é utilizando **git revert HEAD**, de forma que com a utilizaçãao do "HEAD" o último commit realizado será revertido:

```
git revert c2f6c649
```

Após a utilização do comando git revert, o git abrirá sua IDE de utilização para editar o commit de reversão, da seguinte forma:

<p align="center"><img src="https://res.cloudinary.com/practicaldev/image/fetch/s--XgoSowmX--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://thepracticaldev.s3.amazonaws.com/i/cjx1x6u5or4k0x7ftnxn.png" width="400"/></p>

Após a operação,irá aparecer a mensagem de confirmação de reversão do commit.

```
[main 0967249] Revert "adicionando meta dados"
 1 file changed, 1 deletion(-)
```

#### Erro

Caso ocorra algum erro durante o processo de reversão e queira cancelar a operação utilize o comando:

```
git revert --abort
```

## Git Squash
Permite combinar vários commits no histórico da branch para um só. Isso auxilia na visualização do histórico.
Como demonstrado no Rebase interativo, ele é utilizado na parte interativa onde se escolhe o que fazer com cada commit, a partir do rebase --i juntamente com o hash:

``` git rebase -i 5ebadcd ```

Após executar este comando será aberto um arquivo temporário para podermos fazer as alterações desejadas, o arquivo será similar a este abaixo:

``` 
  pick 2a71632 Adicionado Nome   
  pick 742bda9 Adicionado Sobrenome  
  pick e253476 Adicionado Idade  
  pick 4d03037 Adicionado Cidade 

 Rebase 5ebadcd..4d03037 onto 5ebadcd  
  
 Commands:  
  p, pick = use commit  
  r, reword = use commit, but edit the commit message  
  e, edit = use commit, but stop for amending  
  s, squash = use commit, but meld into previous commit  
  f, fixup = like "squash", but discard this commit's log message  
  x, exec = run command (the rest of the line) using shell  
  
 These lines can be re-ordered; they are executed from top to bottom.  
  
 If you remove a line here THAT COMMIT WILL BE LOST.  
  
 However, if you remove everything, the rebase will be aborted.  
  
 Note that empty commits are commented out
```
### Como queremos que os 4 commits sejam "Squashados" somente no primeiro, iremos: 
```
  pick 2a71632 Adicionado Nome   
 squash 742bda9 Adicionado Sobrenome   
 squash e253476 Adicionado Idade  
 squash 4d03037 Adicionado Cidade 
 ```

As linhas dos commits 742bda9, e253476 e 4d03037 foram mudadas para squash, portanto serão combinados ao commit que possui a o nome pick(2a71632 - Nome)