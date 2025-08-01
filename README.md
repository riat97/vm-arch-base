# VM Base Arch Linux com XFCE4 no VirtualBox

Este repositório documenta o processo de criação de uma máquina virtual base com Arch Linux usando o ambiente gráfico XFCE4, instalada via 'archinstall'. Essa VM servirá como base para clones com diferentes finalidades, como sandbox e pentest.

---

## Objetivo

Criar uma VM base leve e funcional com Arch Linux + XFCE4, configurada para personalização futura.

---

## Requisitos

- VirtualBox instalado (versão X ou superior)  
- ISO oficial do Arch Linux (https://archlinux.org/download/)  
- Máquina com pelo menos 4 GB de RAM e 20 GB de disco disponíveis  

---

## Passo a passo da instalação

### 1. Configuração da VM no VirtualBox

- Memória RAM: 4 GB  
- CPUs: 2  
- Disco: 20-40 GB VDI (dinâmico)  
- Vídeo: 128 MB  
- Rede: NAT  

---

### 2. Boot pela ISO do Arch Linux

- Baixe a ISO oficial e monte na VM  
- Inicie a VM e acesse o ambiente live  
- Configure o layout do teclado para brasileiro ABNT2 no instalador  

---

### 3. Instalação com 'archinstall'

- Execute:  
  'archinstall'  
- Escolha o layout de teclado: 'br-abnt2'  
- Use esquema de partição padrão (melhor desempenho)  
- Filesystem: ext4  
- Swap: ativado em zram (padrão)  
- Inicializador de boot: GRUB ou Limine  
- Perfil: desktop (XFCE4)  
- Configuração de rede: ativar NetworkManager  
- Pacotes adicionais: instalar só os essenciais, resto fica para depois  

---

### 4. Primeiro boot e pós-instalação inicial

- Remova a ISO do Arch no VirtualBox para evitar boot no instalador novamente  
- Reinicie a VM  
- Faça login com o usuário criado (ou root, se for o caso)  

---

### 5. Configuração pós-login

- Atualize o sistema:  
  'sudo pacman -Syu'  
- Instale os pacotes básicos essenciais:  
  'sudo pacman -S nano curl wget networkmanager sudo'  
- Habilite e inicie o NetworkManager:  
  'sudo systemctl enable NetworkManager'  
  'sudo systemctl start NetworkManager'  
- Caso esteja usando VirtualBox, instale as ferramentas de integração:  
  'sudo pacman -S virtualbox-guest-utils'  
- Crie um usuário comum com permissões sudo (se ainda não criado):  
  'sudo useradd -m -G wheel seu_usuario'  
  'sudo passwd seu_usuario'  
- Configure sudo para o grupo wheel:  
  'sudo EDITOR=nano visudo'  
  Descomente a linha:  
  '%wheel ALL=(ALL) ALL'  

---

### 6. Testes finais

- Teste a conexão de rede:  
  'ping -c 4 google.com'  
- Teste o ambiente gráfico, reinicie o sistema e veja se o XFCE inicia corretamente  

---

## Referências

- [Arch Linux Installation Guide](https://wiki.archlinux.org/title/Installation_guide)  
- [Archinstall](https://archlinux.github.io/archinstall/)  
- [XFCE](https://www.xfce.org/)  
- [VirtualBox](https://www.virtualbox.org/)  
