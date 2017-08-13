Como Instalar o Linux para o Raspberry

Baixar Imagem do LINUX 
- Ter um imagem do linux que se deseja instalar no PC. Por exemplo, versão do Raspbian L versão do linux no site raspberrypi.org. Não esquecer de descompactar o arquivo com a imagem


Preparar o Cartão SD
- Rodar comando "df -h"
- Verificar todas as partições do cartão SD e utilizar o comando "umount /dev/nome_da_partição" em cada uma delas. Por exemplos, cartao com as partições sdb1 e sdb2, executar os comandos "umount /dev/sdb1" e 
"umount /dev/sdb2"


Copiar/Gravar imagem no cartão
- Ir para o diretório em que esta salva a imagem. Normalmente na pasta Downloads (Comando "cd" bem útil)
- Utilizar o comando "ls" para verificar o nome correto da imagem
- Executar o comando "dd bs=4M if=nome_da_imagem.img of=diretório_do_dispositivo". Substituir "nome_da_imagem" por exatamente o nome do arquivo verificado no passo anterior e, "diretório_do_dispositivo" pelo nome do cartão SD sem o número da partição que foi utilizado na etapa anterior (sdb,sda,sdd). Como exemplo temos:
""dd bs=4M if=2017-02-16-raspbian-jessie.img of=/dev/sdb"
- Para acompanhar o progresso de gravação da imagem no cartão:
    -abrir outro terminal e executar o comando "pkill -USR1 -n -x dd"
   - acrescentar "status=progress" ao comando de gravação, por exemplo:-
	"dd bs=4M if=2017-02-16-raspbian-jessie.img of=/dev/sdb status=progress"
Finalizando assim o processo de gravação e preparação da imagem.


Utilizando pela primeira vez o Raspberry Pi com Raspbian ou equivalente
- Além de colocar o cartão SD, é necessário conectar um teclado USB e também um monitor com entrada HDMI
- Ao ligar o Raspberry, o terminal do linux irá aparecer na tela com diversas mensagens de inicialização do sistema, ao fim, será requisitado login e senha. Normalmente o login é "pi" e a senha é "raspberry" no caso de uma imagem nova
- Execute os comandos "sudo apt-get update" e "sudo apt-get upgrade" para atualizar todos os programas


Expandindo a Imagem no Cartão de Memória
Se voce apenas seguiu os passos desse tutorial, o sistema operacional instalado não estará ocupando todo o espaço disponivel no cartão SD
- Execute o comando "sudo raspi-config"
- Irá aparecer um menu com diversas opções do raspberry, logo a primeiro é "Expand Filesystem", selecione essa opção e confirme
- Após expandir o cartão vá em "Finish" e o Raspberry sofrerá um reboot aplicando todas as mudanças

Finalmente, esta pronta a instalação do Raspberry PI


SSH e Acesso Remoto

Habilitando  o SSH
- Semelhante ao processo de expandir a imagem do cartão, execute o comando "sudo raspi-config"
- Selecione a opção 8 "Configure advanced settings"
- Selecione a opção A4 "SSH" e habilite o SSH
- Recomendo realizar o mesmo procedimento e habilitar SPI e outras formas de comunicação disponiveis
- Vá em "Finish" e o Raspberry sofrerá um reboot aplicando todas as mudanças

Agora não é mais necessário conectar um teclado e uma tela ao Raspberry, voce pode utiliza-lo remotamente através do terminal do seu PC. Para isso, são necessários ainda alguns passos:


Nmap - Encontrando o Raspberry na rede
- Caso não tenha ainda instalado, instale a função nmap no seu PC através do comando "apt-get install nmap" ou "sudo apt-get install nmap."
- Verifique o ip da sua rede, o comum é 192.168.x.xx, ou seja, 192.168 é comun para todos os dispositivos
- Execute o comando "sudo nmap -p22 --open 192.168.0.0/21", substituindo "192.168" pela parte encontrada no item anterior
- Após algum tempo, irá aparecer uma lista de diversos dispositivos disponiveis na rede. Procure por "Raspberry Pi Foundation" ou algum outro nome com "Raspberry Pi" e anote o seu IP
Obs: se voce souber o IP do Raspberry, não é necessário todo o procedimento com o Nmap, é possivel consultar o IP pelo terminal do próprio Raspberry Pi executando o comando "ip addr show" e verifcando o IP após inet"




Conectando via SSH
- Sabendo o IP do seu Raspberry, execute o comando "sudo ssh nome_RPI@IP_RPI", substituindo "nome_RPI" pelo nome do dispostivo (caso não tenha mudado o nome, será simplesmente "pi") e "IP_RPI" pelo o IP encontrado para o Raspberry PI

Saindo do SSH
- Para sair do SSH execute o comando "exit" ou "sudo shutdown -h now" para desligar o Raspberry e consequentemente sair do SSH


Referências:
https://www.raspberrypi.org/documentation/installation/installing-images/linux.md
