---
id: servicosrede
title: Serviços de Rede
---

## REDE 
Usamos alguns comandos para inicializar, parar e reinicializar serviços de rede entre outros, escolha o serviço que deseja e logo em seguida dê o comando, siga o exemplo abaixo:

```
/etc/init.d/firewall start 
/etc/init.d/firewall stop 
/etc/init.d/firewall restart
```
lembre-se que isso é apenas um exemplo logo abaixo estão os comandos de serviço de rede, executamos sempre que validamos a situação da filial
<img src="../img/servicosrede.png" alt="" style="float:right;width:350px">
* links **mpls e adsl** estão OK!
* vpn's OK!
* não a perda de pacotes

então executamos os comandos abaixo:

```
/etc/init.d/bind9 restart
/etc/init.d/xineted restart
/etc/init.d/squid3 restart
/etc/init.d/squid restart 
```
## MPLS
Se ao verificar no splink e identificar o link mpls false execute os comandos abaixo para limpar os dados da rede
```
pcs resource cleanup 
pcs resource restart dhcp
pcs resource enable dhcp 
/etc/init.d/isc-dhcp-server start
```
## SPEED TESTE
Comando usado para verificar a velocidade de internet dos links 

`speedtest-cli --source (ipdolinkparateste)`

## SPLINK
Serviço para monitorar a situação dos links ativos nas filiais e a perda de pacotes.

Comando para identificar situação do serviço splink log.

`tail -f /var/log/splink.log`

[Imagem a ser inserida]

* Primeiro item a ser observado é o nome/tipo do link, por exemplo **vpn, oiadsl, oimpls, etc...**. Informações importantes sobre este link ADSL são verificadas no [Sniffer](http:://sniffer.novomundo.com.br)

* A segunda coisa é o **Status/Situação** do link, e este é demostrado pelo atributo **OK**, se este estiver constando **true** significa que o circuito está operante, se estiver **false** significa que temos problemas.

O primeiro teste a se fazer é verificar se os aparelhos 'Modem' se está com as led's acessas everificar se o cabo de rede está conectado ao Switch. Após essa verificação e a identificação de qual link está **false** faça os procedimentos de testes abaixo:

* Desligar ADSL (teste: portal vtrine e caixa)
* Ligar ADSL e desligar MPLS (teste: portal vtrine e caixa)


Verifique quantos links de operadoras possam ter no local, use o Sniffer para te auxiliar [Sniffer](http:://sniffer.novomundo.com.br)

Se for constatado algum link com problemas abra um chamado para Operadora, anote o número do protocolo passado por eles e adicione no chamado do GLPI.

### Perda de Pacotes

Splink ajuda você a identificar a perda de pacotes.

**Monitoramento**
```
tail -f /var/log/splink.log | grep "INFO.*att" | grep -v "att: 0"
```
**Histórico**
```
cat /var/log/splink.log | grep "INFO.*att" | grep -v "att: 0" | less 
```

## DHCP 
O DHCP, **Dynamic Host Configuration Protocol** (protocolo de configuração dinâmica de host), é um protocolo de serviço TCP/IP que oferece configuração dinâmica de terminais, com concessão de endereços IP de host, máscara de sub-rede, default gateway (gateway padrão), número IP de um ou mais servidores DNS, sufixos de pesquisa do DNS e número IP de um ou mais servidores WINS.

O `dhcpd.hosts` é onde se encontra a lista de IP's configurados para equipamentos da loja conectados no servidor, são eles: 
* Impressora
* DVR's 
* Alarmes 
* AP's 
* Switches gerenciáveis 
* RFS 6000 ( VALIDAÇÃO DO FUNCIONAMENTO DOS COLETORES ).

### Recuperação dos hosts
Pode acontecer, em raros casos, onde o hosts de uma filial se apaga e quando é necessário puxar as configurações do servidor os aparelhos conectados não respondem. Para resolver esse problema precisamos procurar nos arquivos de temporários um arquivo hosts salvo com as configurações corretas da filial, assim devemos realizar os passos abaixo.

Acesse o servidor em questão via ssh, e então:
1. Confirme se o hosts está em branco:
`cat /etc/dhcp/dhcpd.hosts`

2. Acesse a pasta de temporários no servidor
`cd /scripts/tmp/`

3. Dê o seguinte comando:
`ls -l dhcpd.hosts_ANO/MÊS` (exemplo: `ls -l dhcpd.hosts_201904` para ver os arquivos de abril de 2019)

4. Busque nos vários aquivos que aparecerem aquele que apresenta um valor diferente de 1 na quinta coluna (por exemplo 945) e seja mais recente
[imagem.png](...). O arquivo é aquele que se encontra na última coluna, por exemplo: `dhcpd.hosts_20190409070015`

5. Confirme se esse arquivo não está vazio com o comando:
`cat dhcpd.hosts_20190409070015`

6. Copie o arquivo escolhido para hosts do servidor com o comando: 

    `cp dhcpd.hosts_20190409070015 /etc/dhcp/dhcpd.hosts`

7. Verifique se o arquivo foi copiado para o servidor:
`cat /etc/dhcp/dhcpd.hosts`

8. Reinicie o DHCP
`pcs resource restart dhcp` (Para imagens 2017)

    `/etc/init.d/isc-dhcp-server restart` (Para imagens anteriores a 2017)

9. Sinta-se orgulhoso.

### Fixar um MAC no dhcp
* Acessar um servidor da filial via ssh
    `ssh operacao@srv0000-1`
* Editar o arquivo **dhcpd.hosts**
[imagem.png](...)
* Crie um registro
    `host tipohost-99990-00-local { hardware ethernet 09:ba:ff:09:49:0f; fixed-address 172.11.1.1; }`

#### Regras do nome
* tipohost é o tipo do dispositivo que está sendo configurado, por exemplo: alarme para centrais de alarme, switch para switch, rep para relógios de ponto, imp para impressora, dvr para DVR, etc.
* 9999 é o código do centro de custo com 4 dígitos e zeros à esquerda.
* 00 é um sequencial iniciado em 1 par ao tipo do dispositivo.
* local é uma descrição breve sobre onde o dispositivo está instalado, por exemplo: principal para rack principal, brigadista se estiver no rack do brigadista, caixa se estiver na área de caixas, financeiro se estiver no departamento financeiro, etc.
#### Regras gerais
* Não utilizar _ (underline) no nome do host.
* Não utilizar letras maiúsculas.
* Não utilizar espaço.
* Observar o IP padrão para o tipo de dispositivo na página CheckList de Pré Natal.
#### Salvar
Pressione as teclas ctrl+k+x

#### Restart o dhcp
`pcs resource restart dhcp`

#### Caso não tenha o MAC do dispositivo
Se não tiver o MAC do dispositivo, configure-o para usar DHCP e no servidor utilize o comando abaixo para ver quem esta solicitando IP:
`tail -f /var/log/dhcp.log`
[imagem.png](...)
#### Ativação do DHCP
```
pcs resource restart dhcp
pcs resource enable dhcp 
pcs resource disable dhcp
pcs resource --help - em caso de dúvidas use
```

## VPN

> As configurações das novas vpns seguirão o padrão de duas vpns. Para nossa conexão **(vpnnm01 e vpnnm02)** e duas para conexão com a Oracle **(vpndc01 e vpndc02)**

Em caso das vpn's estarem down é bom reiniciar o modem ADSL primeiro, logo após reiniciar executar os scripts para derrubar e subir as vpns.

```
derrubar: nm01 
/scripts/openvpn_down.sh /etc/openvpn/openvpn_nm01.ovpn 
subir: nm02
/scripts/openvpn_up.sh openvpn_nm02.ovpn  
derrubar: dc01
/scripts/openvpn_down.sh /etc/openvpn/openvpn_dc01.ovpn
subir: dc02
/scripts/openvpn_up.sh openvpn_dc02.ovpn  
```
## IP ROUTE

Filial não está tendo acesso a sites externos, verifique o ip route no servidor

```
srv0000-1:~$ ip route
10.1.55.33/24 via 172.1.1.1 dev vlan60 
10.1.55.0/24 via 172.1.1.1 dev vlan60 
10.1.55.8/29 via 172.1.1.1 dev vlan60 
10.1.55.0/21 via 10.1.1.8 dev tun1 
```
ao digitar o comando **ip route** a primeira linha teria que estar configurado para um ip via default `default via 192.1.1.1 dev vlan60` para adcionar essa linha basta verificar o último octeto do ip adls no splink, subtrair por -1.
> Exemplo: no splink o link adsl vivo é 192.168.1.**2**, então para adicionar o ip route é 192.168.1.**1**  

então configure  
```
srv0000-1:~$ ip route add default via 192.168.1.1
'verifique'
srv000-1:~$ ip route
default via 192.168.1.1 dev vlan60
10.1.55.33/24 via 172.1.1.1 dev vlan60 
10.1.55.0/24 via 172.1.1.1 dev vlan60 
10.1.55.8/29 via 172.1.1.1 dev vlan60 
10.1.55.0/21 via 10.1.1.8 dev tun1 
```
viu que foi adicionado um ip default ? agora basta validar com a filial e tentar reabrir algum site externo! 