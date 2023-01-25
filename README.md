# Documentação de Git

## Sumário
* [Git Rebase](#git-rebase)
* [Git Cherry Pick](#git-cherry-pick)
* [Git Revert](#git-revert)
* [Git Squash](#git-squash)

## Git Rebase
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

  * **-e:** permite que você edite a mensagem do commit.  

  * **-x:** adiciona uma mensagem no commit copiado avisando que ele é um cherry pick de um outro commit – “cherry picked from commit”.  

  * **–allow-empty:** por padrão, o cherry-pick não permite commits em branco, com esse parâmetro, ele sobrescreve esse comportamento.  

  * **–allow-empty-message:** quando o commit não tem um título, ele é barrado. Assim como no exemplo anterior, esse parâmetro sobrescreve o comportamento.

### Aviso

O Git cherry-pick é um comando muito útil quando bem utilizado, porém ele não pode substituir o git merge e o git rebase. Cada um possui uma situação que se encaixa melhor, mas isso é assunto para um próximo artigo.

Use o cherry-pick só em último caso, cuidado para não sair duplicando commits na sua linha do tempo, use com moderação!


## Git Revert
## Git Squash