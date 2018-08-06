---
layout: post
title:  "eopkg detalhes"
date:   2018-08-06 20:12:00 +0000
categories: Linux
tags: solus help
comments: 1
---

O Solus usa o sistema de gerenciamento de pacotes eopkg para entregar software ao usuário final. 
Abaixo estão alguns comandos básicos para usar o eopkg.

#### Noções básicas de gerenciamento de pacotes.

> Instalando Software  
Você pode instalar um ou mais pacotes usando:
```
sudo eopkg install packagename
```
> Por exemplo:
```
sudo eopkg install gnome-documents gnome-music
```
> Reinstalando Software
Você pode reinstalar um ou mais pacotes usando:
```
sudo eopkg install --reinstall packagename
```
> Por exemplo:
```
sudo eopkg install --reinstall gnome-documents gnome-music
```
> Desinstalando o software
Você pode desinstalar um ou mais pacotes usando:
```
sudo eopkg remove packagename
```
> Por exemplo:
```
sudo eopkg remove gnome-documents gnome-music
```
> Obter informações sobre software
Você pode obter informações sobre software, como sua descrição, versão, tamanho da instalação e muito mais, usando
```
sudo eopkg info packagename
```
> Por exemplo:
```
sudo eopkg info gnome-documents
```
> Atualizando
Você pode atualizar seu sistema usando:
```
sudo eopkg upgrade
```
> Se você quiser apenas atualizar uma parte específica do software no seu sistema, você pode especificar é como abaixo:
```
sudo eopkg upgrade firefox
```
> Procurando
Você pode pesquisar a seleção de software que a Solus fornece usando:
```
sudo eopkg search term
```
> Por exemplo:
```
sudo eopkg search documents
```
> Observe que você não precisa procurar por um nome de software específico, embora você possa fazer isso. Procuramos resumos e nomes de software por padrão.
```
Ferramentas de desenvolvimento base
```
> Se você está querendo compilar software sob o Solus, recomendamos instalar o nosso componente system.devel rodando o seguinte:
```
sudo eopkg install -c system.devel
```
> Isso fornecerá itens como clang, gcc, make, vários sub-pacotes de desenvolvimento e muito mais. Nosso system.devel é similar a pacotes em outros sistemas operacionais, como o essencial da Debian.
```
By: Nilsonlinux. Fonte:  
https://solus-project.com/articles/package-management/basics/en/
