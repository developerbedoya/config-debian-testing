# Configuração inicial
* Colocar o valor `nouveau.modeset=0` no parâmetro `GRUB_CMDLINE_LINUX` arquivo `/etc/default/grub`
* Executar `sudo update-grub`

# Pacotes debian
```
sudo apt install vim-gtk3 mc gdebi synaptic pavucontrol git htop iotop cups qtbase5-dev qt5-quick-demos cmake qtdeclarative5-dev qtcreator gimp
```

# Instalar pacotes baixados
```
sudo gdebi (chrome)
sudo gdebi (code)
sudo gdebi (teams)
```

# Habilitar icones systray
```
sudo apt install gnome-shell-extension-top-icons-plus
```
e depois habilitar no gnome-tweak-tool

# Configurar microfone
* Colocar no final do arquivo `/etc/pulse/default.pa`:
```
load-module module-remap-source source_name=record_mono master=alsa_input.pci-0000_00_1f.3.analog-stereo master_channel_map=front-left channel_map=mono
set-default-source record_mono
```
* Reiniciar pulseaudio:
```
pulseaudio -k
pulseaudio --start
```

# Resolver problema de congelamento do computador ao copiar arquivos
* Criar arquivo `/etc/sysctl.d/vm-dirty.conf`:
```
# Shrink the disk buffers to a more reasonable size. See http://lwn.net/Articles/572911/
vm.dirty_background_bytes = 16777216
vm.dirty_bytes = 50331648
```

# Mudar swappiness
```
sudo sysctl vm.swappiness=10
echo "wm.swappiness=10" | sudo tee -a /etc/sysctl.conf
```

# Instalar kvm e libvirt
* Instalar, e depois reiniciar a máquina:
```
sudo apt install qemu-kvm bridge-utils virt-manager libosinfo-bin
```
* Depois, iniciar a rede `default` e marcá-la como de início automático:
```
sudo virsh net-start default
sudo virsh net-autostart default
```

# Colocar fontes do Windows
* Copiar fontes
```
mkdir ~/.fonts
cp ~/Downloads/noarch/windows_fonts/* ~/.fonts
fc-cache -f -v
```

* Resolver renderizado no libreoffice
```
mkdir -p ~/.config/fontconfig
```
Copiar no arquivo `~/.config/fontconfig/fonts.conf`
```
<match target="font" >
  <edit name="embeddedbitmap" mode="assign">
    <bool>false</bool>
  </edit>
</match>
```

# Instalar Source Code Pro
```
mkdir -p ~/.fonts/adobe-fonts
git clone https://github.com/adobe-fonts/source-code-pro.git ~/.fonts/adobe-fonts/source-code-pro
fc-cache -f -v
```

# Instalar impresora Epson
* Instalar pacotes que estão na pasta epson

* Fazer gambiarra para deixar executar os programas da impresora
```
sudo ln -s /lib64/ld-linux-x86-64.so.2 /lib64/ld-lsb-x86-64.so.3
sudo apt install libcupsimage2
```
