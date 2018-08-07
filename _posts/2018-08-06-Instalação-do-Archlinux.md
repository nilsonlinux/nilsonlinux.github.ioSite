---
layout: post
title:  "Instalação do Archlinux"
date:   2018-08-06 11:09:13 +0800
categories: Linux
tags: Instalação
comments: 1
---

Instalação e Configuração do Arch Linux  
O Arch Linux é considerada para usuários mais avançados, por conta de sua filosofia de desenvolvimento. Além disso, o Arch Linux é simples, flexível e considerada UNIX-like.  
Site Arch Linux: www.archlinux.org  

Boot Arch Linux (x86_64) — Dar o boot na versão de x64 bits  
Boot existing OS — Fazer boot no atual sistema (Se já existir)  
Run Memtest86+ (RAM test) — Fazer avaliação da memória  
Hardware Information (HDT) — Informações de Hardware  
Reboot — Reiniciar o Computador  
Power Off — Desligar o Computador  

Você já está logado como # (root)  

################ ARCH-LINUX ##############  

1- Mudar teclado para abnt2 (PT-BR)  
```
loadkeys br-abnt2  
```   

2- Mudar a fonte do terminal.  
```
setfont lat0–16  
```   

3- Configurar locale (Localização)  
```
nano /etc/locale.gen  
```   

descomentar essa linha:  
```
pt_BR.UTF-8 UTF-8  
```  

Salvar “ctrl+o” depois (Enter) e sair “ctrl+x”  

4- Criar o aquirvo de conf de linguagem  
```
locale-gen  
```   
```
export LANG=pt_BR.UTF-8  
```  

5- Caso sua internet seja cabeada.  
```
dhcpcd  
```  

6- Caso sua rede seja wireless.  
```
wifi-menu  
```  

7- Testar a Conectividade.  
```
ping -c 3 www.google.com  
```  

8- Descobri qual disco rígido foi detectado:  
```
dmesg | grep sd  
```  

9- Configurar as partições no disco ( No meu caso, usei um disco de 20GB)  
```
cfdisk /dev/sda  
```  
 ‘sda’ (Primeiro disco rígido SATA) ou ‘sdb’ (Segundo disco rígido SATA)  

sda1 * 9G /  
sda2 1G swap  
sda3 10G /home  
10- Escrever/Write as mudanças nas partições.  

Escrever/Write — Sim/Yes  
Quit/Sair  

11- Para formatar as partições com um sistema de arquivos ext4:  
```
mkfs.ext4 /dev/sda1  
mkfs.ext4 /dev/sda3  
```  

12- E para formatar e ativar a partição de swap:  
```
mkswap /dev/sda2  
swapon /dev/sda2  
```  

Para verificar se a partição swap está funcionando, utilize o comando free ou swapon  
```
swapon -s  
free -h  
```  

13- Primeiro, monte a partição raíz em /mnt.  
```mount /dev/sda1 /mnt```  

14- Monte então a partição destinada ao /home e outras separadas para o /boot, /var, etc, caso desejar:  
```
mkdir /mnt/home  
mount /dev/sda3 /mnt/home  
```  

15- No caso da partição /boot ser separada:  
```
mkdir /mnt/boot  
mount /dev/sdaX /mnt/boot  
```  

16- Para ver o layout de particionamento atual:  
```
lsblk /dev/sda  
```  

17- Instalar o sistema no diretório sda  
```
pacstrap /mnt base base-devel
```  
 
18- Gerar arquivo fstab (FSTAB: File System Table)(Se preferir adicione a opção -U (UUIDs) ou -L (labels))  
```
genfstab -U -p /mnt/ >> /mnt/etc/fstab
```  

19- Caso você queira editar o arquivo fstab.  
```
nano /mnt/etc/fstab
```  

20- Criar ambiente chroot ( Agora podemos fazer todos os procedimentos estando no diretório “/”, não precisando indicar o /mnt.) (CHROOT: Change Root)  
```
arch-chroot /mnt /bin/bash
```  

21- Configurar locale (Localização)  
```
nano /etc/locale.gen
```  

descomenta essa linha:  
pt_BR.UTF-8 UTF-8  

Salvar “ctrl+o” depois (Enter) e sair “ctrl+x”  

22- Fazer a leitura daquele arquivo e gerar o locale.  
```
locale-gen
```  

23- Criar o aquirvo de conf de lingua  
```
echo LANG=pt_BR.UTF-8 > /etc/locale.conf  export LANG=pt_BR.UTF-8
```  

24- Se você alterou o mapa do teclado no inicio do processo de instalação, recarregue tal configuração novamente pois seu ambiente mudou.   Exemplo:  
```
loadkeys br-abnt2  
setfont lat0–16
```  

25- Para que tais configurações persistam após um reboot, edite o arquivo vconsole.conf:  
```
nano /etc/vconsole.conf
```  

KEYMAP=br-abnt2  
FONT=lat0–16  
FONT_MAP=  
Salvar “ctrl+o” depois (Enter) e sair “ctrl+x”  

26- Configurar o fuso-horário  
```
ls /usr/share/zoneinfo/America  
ln -sf /usr/share/zoneinfo/America/Recife /etc/localtime
```  

27- Sincronizando o relógio de hardware com o do sistema  
```
hwclock — systohc — utc  (UTC (recomendado)
```  

28- Configurando o repositório. (Se você instalou o Arch Linux x86_64, é recomendado que você habilite o repositório [multilib], bem (para ser capaz de executar aplicativos de 32-bits em seu sistema 64-bits)  
```
nano /etc/pacman.conf
```  

Descomentar essas linhas.  

[multilib]  
include = /etc/pacman.d/mirrorlist  
Salvar “ctrl+o” depois (Enter) e sair “ctrl+x”  
29- Sincronizar os repositórios.  
```
pacman -Sy
```  

30- Dar um nome para a máquina.  
```
echo archlinux > /etc/hostnam
```  

31- Adicionando entrada correspondente  
```
nano /etc/hosts
```  

127.0.0.1 localhost.localdomain localhost  
::1 localhost.localdomain localhost  
127.0.1.1 myhostname.localdomain myhostname 

32- Instalando o SUDO e AUTO complemento de comandos e nomes de pacotes.  
```
pacman -S sudo bash-completion
```  

33- Baixar e instalar o GRUB no computador.  
(BIOS)  
```
pacman -S grub  
grub-install — target=i386-pc — recheck /dev/sda  
cp /usr/share/locale/en\@quot/LC_MESSAGES/grub.mo /boot/grub/locale/en.mo  
```  

Dica: Para a busca automática de outros sistemas operacionais em seu computador, instale o pacote os-prober (pacman -S os-prober) antes de rodar o próximo comando.  

34- Crie um ambiente ramdisk inicial.  
```
mkinitcpio -p linux
``` 

35- Install Microcode  
Para processadores Intel com carregador de inicialização grub:  
```
pacman -S intel-ucode
```  
Para os processadores AMD instalar o pacote linux-firmware  

36- Gerar arquivo de configuração do GRUB.  
```
grub-mkconfig -o /boot/grub/grub.cfg
```  

37- Criar usuario e definir senha  
```
useradd -m -g users -G wheel,storage,power -s /bin/bash joao  
passwd joao  
```  

38- Definir a senha de root  
```
passwd root
```  

39- Edite o arquivo sudoers:  

```
nano /etc/sudoers
```  

Descomente a opção  
   
%wheel ALL=(ALL) ALL  

 wheel ALL=(ALL) ALL  
  
40- Instalar componentes do Wi-Fi.  
```
pacman -S wpa-supplicant networkmanager net-tools  
systemctl enable NetworkManager  
```  

Em seguida, você pode configurar Ethernet ou Wifi:  
check device name  
```
ifconfig -a  
ifconfig wlp2s0 up  
```  

41- Se você estiver instalando Arch Linux em um laptop, então você também precisa de apoio para trackpad, então instalar o pacote “synaptics”:  
```
pacman -S xf86-input-synaptics
```  

42- Sair do modo chroot (ctrl+d ou exit), voltamos para o CD.  

43- Desmontar as partições.  
```
umount /mnt/home  
umount /mnt
```  

44- Reiniciar o Sistema.  
```
reboot
```  

45- Vamos escolher opção “Arch-Linux”, pronto o Arch-Linux está instalado.  

Finalizamos a Instalação do Arch Linux ;)  
Após a instalação do Arch Linux a única coisa que os usuários veem é uma linha de comando sem qualquer servidor X, então o usuário deve instalar o X server e uma área de trabalho e alguns outros aplicativos para fazer seu trabalhos diários.  

Interface de usuário básica para configuração de rede  
nmtui  

1- Por ter GUI no seu sistema, que você precisa instalar o servidor X e eles podem ser instalados no sistema no comando a seguir (Xorg é o servidor de exibição mais popular entre os usuarios Linux.).  
```
$ sudo pacman -S xorg-server xorg-xinit xorg-apps gvfs-mtp sshfs
```  

2- Verificar a placa gráfica no Linux:  

```
lspci | grep VGA
```  

Use a saída do comando acima para determinar qual driver você precisa. ( Instale o que for referente ao seu)  

```
pacman -S virtualbox-guest-utils — para o virtualbox  
pacman -S xf86-video-amdgpu — para placas amd-radeon  
pacman -S xf86-video-nouveau — para placa de vídeo Nvidia  
pacman -S xf86-video-intel — para drivers da intel  
```  

Eu usei este, use também para sua referencia.  
```
pacman -S xf86-video-intel  
```  

3- Próxima coisa que precisa e dos ultilitarios de som.  
```
sudo pacman -S pavucontrol alsa-firmware alsa-utils alsa-plugins pulseaudio-alsa pulseaudio
```  

4- Depois de instalar o servidor X você precisa de um ambiente de Desktop ou um Gerenciador de janelas para fazer seus trabalhos com isso!  

Nota: Instalar pacotes de grupo Extra é opcional!  
[Instalar xfce4 Desktop Environment]  
```
$ sudo pacman -S xfce4 xfce4-goodies
```  
[Instalar Budgie Desktop Environment]  
```
$ sudo pacman -S budgie-desktop
```  
[Instalar GNOME Desktop Environment]  
```
$ sudo pacman -S gnome gnome-extra
```  
[Instalar Cinnamon Desktop Environment]  
```
$ sudo pacman -S cinnamon nemo-fileroller
```  
[Instalar KDE Desktop Environment]  
```
$ sudo pacman -S plasma
```  
[Instalar Mate Desktop Environment]  
```
$ sudo pacman -S mate mate-extra
```  
[Instalar Deepin Desktop Environment]  
```
$ sudo pacman -S deepin deepin-extra
```  
[Instalar Enlightenment Desktop Environment]  
```
$ sudo pacman -S enlightenment
```  
[Instalar LXDE Desktop Environment]  
```
$ sudo pacman -S lxde
```  
[Instalar LXQT Desktop Environment]  
```
$ sudo pacman -S lxqt
```  
5- No meu caso vou instalar o XFCE ❤  
```
sudo pacman -S xfce4 xfce4-goodies
```  

Instalação Gerenciador de exibição LightDM no Arch-Linux  

6- Existem muitos do Gerenciador de exibição para usar como XDM, slim e etc… mas meu favorito é lightdm porque é rápido e personalizável.  

7- Para instalar LightDM use o seguinte comand  
```
pacman -S lightdm lightdm-gtk-greeter
```  

8- Você pode instalar o pacote para ser capaz de personalizar seu LightDM por uma aplicação gráfica na sequência:  
```
pacman -S lightdm-gtk-greeter-settings
```  

9- Agora ative o serviço:  
```
systemctl enable lightdm
```  

10- Vamos Reiniciar  
```
reboot
```  

[Instalar, Iniciar & Ativar lxdm Display Manager]  
```
$ sudo pacman -S lxdm```  
$ sudo systemctl start lxdm.service  
$ sudo systemctl enable lxdm.service  
```  
[Iniciar & Ativar GDM Display Manager]  
```
$ sudo systemctl start gdm.service  
$ sudo systemctl enable gdm.service  
```  
[Instalar, Iniciar & Ativar GDM Display Manager]  
```
$ sudo pacman -S gdm```  
$ sudo systemctl start gdm.service  
$ sudo systemctl enable gdm.service  
```  
Instalação Sem Gerenciador de Login # ( Opcinal )  
Use o comando correspondente para incluir no arquivo ~ / .xinitrc e instale o GUI correspondente:  

1-Próximo comando.  
```
cp /etc/X11/xinit/xinitrc ~/.xinitrc
```  

2- Proximo comando.  
```
nano ~/.xinitrc
```  
 
3- (comentar a seguinte linha com “#” )  
```
exec xterm -geometry (…) -name login  
```  

4- Adicionar a seguinte linha logo abaixo.  
```
exec startxfce4
```  
 
5- Salve (CTRL+O), confime (ENTER) e saia (CTRL+X)  

6- Finalizar (Saia do modo #root)  
```
$ startxfce4
```  


Xfce:  
“exec startxfce4”  
Gnome:  
“exec gnome-session”  
Cinnamon:  
“exec cinnamon-session”  
Mate:  
“exec mate-session”  
Unity:  
“exec unity”  
Openbox  
“exec openbox-session”  
I3:  
“exec i3”  
Awesome:  
“exec awesome”  
##########Inicialmente no Ambiente de Trabalho##########  

1 -Entre como SuperUsuário #  
```
$ su
```  

2- Colocando as pastas de usuários:  
```
pacman -S xdg-user-dirs  
xdg-user-dirs-update  
```  

3- Ja no ambiente X aogra vou configurar teclado abnt2 no ambiente X:  
```
localectl set-x11-keymap br abnt2
```  

4- Baixar o ícone de gerenciamento de rede: (opcional + recomendado)  
```
pacman -S network-manager-applet
reboot  
```  

5- Bluetooth:  

Bluetooth, digite o seguinte comando no Terminal para instalar os pacotes:  

```
sudo pacman -S bluez blueman bluez-utils
```  

Agora inicie o módulo btusb:  

```
modeprobe btusb
```  

Habilitar e iniciar o serviço de bluetooth:  

```
sudo systemctl enable bluetooth && sudo systemctl start bluetooth
```  

Feito!  

6- AUR Repo:  

Alguns pacotes tais como Kazam, i3blocks e etc não podem ser encontrados no repositórios Main, para nós deve instalá-los de AUR e para fazer também precisamos adicionar endereço AUR no final do arquivo /etc/pacman.conf.  

Yaourt fornecer experiência muito suave de pesquisa interativa e instalar a partir do AUR.  

Primeiro, abra este arquivo com o editor nano:  

```
sudo nano /etc/pacman.conf
```  

Agora adicione essas linhas na parte inferior do arquivo:  

[archlinuxfr]  
SigLevel = Never  
Server = http://repo.archlinux.fr/$arch  
Agora salve as alterações (CTRL + O)+ ENTER, e atualize o seu sistema pelo seguinte código:  
```
sudo pacman -Syu
```  

Yaourt é a ferramenta que permite que os usuários baixe e instale os pacotes do repositório não-oficial, então, instalar esta ferramenta pelo seguinte comando:  
```
sudo pacman -S yaourt
```  

Teste Yaourt, para fazer isso você só precisa instalar um pacote com isso como um exemplo instalar pacote Kazam com isso:  

```
$ yaourt -S kazam
```  

Nota: Os usuários não deveriam usar sudo enquanto estiverem usando o comando yaourt.  
 
Para atualizar os pacotes instalados a partir do AUR:  

```
$ yaourt -Suy — aur — noconfirm
```  

####################FIM ####################  