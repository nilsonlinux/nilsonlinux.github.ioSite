---
layout: post
title:  "comandos bash"
date:   2018-08-06 20:55:32 +0000
categories: Linux
tags: terminal bash
comments: 1
---

Aprenda como criar comandos bash personalizados em menos de 4 minutos

Exemplo de aliases customizados para comandos bash
Neste artigo, ensinarei como você pode criar atalhos personalizados (aliases) para comandos bash e também como executar vários comandos por um comando bash.

TL; DR - A primeira parte descreve por que os aliases são importantes e quanto tempo você pode economizar, e assim por diante, se você quiser apenas aprender como configurar seus próprios aliases, vá para a etapa 1 .
Aumentar o desempenho
À medida que crescemos (eu sei, o tempo voa!), Temos mais responsabilidades, como cuidar da família, administrar as finanças, passar tempo com os entes queridos, levar as crianças ao jardim de infância e outras coisas relacionadas à vida adulta.

O tempo é um fator importante que influencia muito o desempenho no trabalho, especialmente se você for um programador. Com todas essas novas responsabilidades e menos tempo fazendo as coisas que você quer aprender, é importante ser eficiente.

Se você quer se tornar um desenvolvedor web melhor, começar seu próprio negócio, ensinar aos outros, ou simplesmente melhorar suas habilidades de desenvolvimento, postarei dicas e truques semanais nos últimos idiomas de desenvolvimento web.
Mundo programadores
Como programadores, que muitas vezes encontramos correndo mesmo o bash comandos muitas vezes, como cd .., ls -lou pwdao longo de um projeto de desenvolvimento. A execução desses comandos uma vez por semana não afeta a eficiência, mas duas vezes por dia em uma perspectiva de longo prazo.

Alguns dos comandos bash são curtos e outros são longos. Alguns deles são difíceis de lembrar e outros não. O objetivo é aumentar o fluxo de trabalho (eficiência), o que significa que você pode criar comandos declarativos (código legível), fáceis de lembrar e rápidos de escrever.

Tenha em mente que a idéia não é criar aliases para cada comando de terminal, mas aqueles que você usa repetidamente. E também, esteja ciente de que alguns aliases podem ser palavras reservadas, então teste-as antes de sobrescrever erroneamente um comando crítico.
Encurte os comandos do git
Fiz um teste simples para ilustrar quanto tempo é necessário para fazer alterações no Github. Em média, leva cerca de 20 a 25 segundos para o programador médio empurrar as alterações para o github.com .

# Test 
git add. 
git commit - m "pequenas alterações" 
git push -u origem mestre
Digamos que você faça pelo menos 15 git pushsemanas por semana, e o tempo total de envio de alterações para um repositório leva cerca de 20 segundos.

Uma semana levaria 5 minutos
Um mês levaria 20 minutos
Um ano levaria 4 horas
E se substituirmos esses 3 comandos por um apelido lazyman "minor changes", reduziremos de 20 segundos para 5 segundos.

Uma semana levaria 1,25 minutos
Um mês levaria 5 minutos
Um ano levaria 1 hora.
Em geral, aumentamos o desempenho em 75% (um fator de 3). Este foi apenas um exemplo simples, mas imagine quanto tempo podemos salvar, por exemplo, se executar comandos como run apache server && run tests && report data && closeou gcc project-source-code.c -o executable-file-name15-30 vezes por dia.

Como eu medi o aumento de desempenho? (para nerds)
# Formula
((old - new) / old) * 100%
= ((20 sec - 5 sec) / 20 sec) * 100%
= 75 % (performance increase) 
Antes de criar aliases
Para criar aliases, geralmente os colocamos em ~/.bashrcarquivo, este é um arquivo oculto no seu diretório pessoal que você pode acessar de qualquer lugar no seu terminal. No entanto, uma boa prática é manter os arquivos do sistema separados do caso de uso pessoal. Por esse motivo, vamos criar um novo arquivo chamado ~/.custom_aliasese colocar todos os aliases lá. Além disso, lembre-se de que, sempre que você adicionar um novo alias, execute, source ~/.custom_aliasescaso contrário, os aliases não funcionarão.

Etapa 1 - criar um arquivo custom_aliases
Todos os aliases que você cria devem ser armazenados nesse arquivo.

# criar arquivo 
toque ~ / .custom_aliases
Etapa 2 - Abra o arquivo custom_aliases
Abra o arquivo através de um editor de texto, através de geditou code(código do Visual Studio), ou o que você preferir.

Código do Visual Studio (se instalado)

# abre o 
código do arquivo ~ / .custom_aliases
Gedit

# abre o arquivo 
gedit ~ / .custom_aliases
Etapa 3 - Criar atalhos (aliases)
Vamos criar um alias simples que imprima “Bem-vindo John Doe” quando digitarmos bem-vindos no terminal bash.

alias welcome = 'echo "Bem-vindo $ USER."'
Etapa 4— Atualizar alterações
Antes de poder executar o comando bash recém-criado, você deve atualizar o custom_aliasesarquivo.

# atualiza a 
fonte do arquivo ~ / .custom_aliases
Passo 5 - Execute o novo comando bash
Digite o seguinte na sua linha de comando preferida.

# linha de comando 
bem- 
vindo> Bem - vindo John Doe.
Bem feito! Agora você criou um arquivo personalizado para colocar aliases, vamos ver quais tipos de comandos você pode criar.

Aliases personalizados para comandos bash (pessoal)
Aqui estão alguns comandos bash que estou usando para aumentar meu fluxo de trabalho.

Boa dica: para manter a estrutura ao adicionar vários aliases, coloque-os em seções, como mostrado no exemplo abaixo, usando comentários.
#
 Alias ​​de Controle de Versão gs = "status git" 
alias gd = "git add." 
alias gp = "git push -u origem mestre"

#
 Alias ​​de diretório diskusage = "df -h" 
alias folderusage = "du -ch" 
alias totalfolderusage = "du -sh"

# Vários  
 alias opencustomaliases = "código ~ / .custom_aliases" 
alias updatecustomaliases = "fonte ~ / .custom_aliases" 
alias updatethenupgrade = " sudo apt-get update && sudo apt-get upgrade"
Tenha em mente que algum sistema operacional (sistema operacional) pode ser diferente, certifique-se de executar esses comandos no terminal e verificar se ele funciona antes de colocá-los no custom_aliasesarquivo.

Executando vários comandos
Você também pode criar um comando bash que execute vários comandos. Há duas maneiras de conseguir isso: crie uma função ou crie um alias.

Exemplo 1 - Criar função
# Vários comandos
função lazyman () { 
    git add. 
    git commit -a -m "$ 1" 
    git push -u origem mestre 
}
Exemplo 2 - criar alias
# Vários comandos
alias lazyman = "git add. && git commit -a -m '$ i' && git push -u origem mestre"
Lembre-se de atualizar o custom_aliasesarquivo executando source ~/.custom_aliasese, em seguida, digite lazyman "First commit".