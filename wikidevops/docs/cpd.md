---
id: cpd
title: Infra #TI
sidebar_label: Servidores
---

Nesta seção estão descritas as normas e procedimentos para solucão de problemas 
relacionados a aplicativos e sistemas Novo Mundo 
<img src="../img/logo2.png" alt="" style="float:right;width:300px"/>

## PRIMÁRIO | SECUNDÁRIO

Para ter acesso aos servidores abra o terminal **konsole** e digite os seguintes comandos:
```
ssh operacao@srv0000-1 ou 2 
```

Substitua os 3 ultimos 000 pela numeração da filial que deseja ter acesso.
```
teste@1c58s8ds99ab:~$ ssh operacao@srv0000-1
operacao@srv0000-1's password:
```
Após esse procedimento digite a senha para ter acesso: **passwd**, em seguida digite ``` sudo su - ``` insira a senha novamente
```
operacao@srv0000-1:~$ sudo su -
[sudo] senha para operacao:
```
Se o servidor primário falhar tente acessar o secundário tente acessar o secudário.
>a função dele é assumir a loja caso o primário dê algum problema

Assim que tiver acesso execute os comando de monitoramento 
[Serviços de Rede](servicosrede.md)

>Caso não consiga ter acesso, siga o procedimento abaixo


## USANDO O PING
Para poder pingar os servidores no seu terminal digite o comando **su**
```
teste@1c58s8ds99ab:~$ su
senha: **************
/home/teste# 
```
```
teste# ping srv0000-1 
teste# ping srv0000-2

1c58s8ds99ab:/home/teste# ping srv0000-1
PING srv0000-1.novomundo.com.br (172.1.1.1) 56(84) bytes of data.
64 bytes from 172.1.1.1 (172.1.1.1): icmp_seq1 ttl=60 time 22.1ms
64 bytes from 172.1.1.1 (172.1.1.1): icmp_seq2 ttl=60 time 24.1ms
64 bytes from 172.1.1.1 (172.1.1.1): icmp_seq3 ttl=60 time 26.1ms
--- srv0000-1.novomundo.com.br ping statistics ---
2 packets transmitted, 2 received, 0% packet loss, time 1001ms
rtt min/avg/max/mdev = 22.100/3223/108/24.117/1.019 ms
```

[O que é e como funciona o Ping ??](cpd.md)

>Certifique-se que ambos estejam UP

Sem acesso e servidores totalmente inoperantes, peça ao colaborador(a) que verifique os equipamentos abaixo, as vezes reiniciando algum destes equipamentos pode ser que volte a funcionar normalmente.
* Servidor Primário 
* Secudário
* Modem 
* Switch

## COMANDO PCS STATUS

Verifica qual é o servidor que está assumindo a filial: ```pcs status```

![pcs status] (imagen a ser inserida)

========================= Inserir mais informações =======================

Para desativar um servidor, que por exemplo esteja sendo dado manutenção utilize:

`pcs cluster standby server1.novomundo.com.br`

`pcs cluster standby server2.novomundo.com.br`

Para ativar novamente, utilize:

`pcs cluster unstandby server1.novomundo.com.br`

## CLUSTER

Ao executar o comando `pcs status` e caso apareça a seguinte mensagem, reinicie os serviços do cluster.

`Erro: Cluster is not currently running on this node`

```
Reiniciar corosync: /etc/init.d/corosync restart
Reiniciar pacemaker: /etc/init.d/pacemaker restart
Reiniciar pcsd: /etc/init.d/pcsd restart
```

## DATA SERVER

Problemas mais relatados são:

 Erro ao acessar um específico dataserver, um Analista sempre vai perguntar quais testes já foram efetuados. Segue a lista a baixo de como proceder com esse tipo de situação.
* Valide o acesso de sites internos da loja como Portal, Vtrine entre outros, se o usuário estiver Home Office faça o mesmo procedimento.
* Valide a senha que eles está tentando o acesso. 
* Verifique o tipo de erro que aparece ao tentar acessar o dataserver.

Mensagem de erro 
> O Windws não pode acessar o srv0933-1.novomundo.com.br/martins **"erro de rede "**

Tente acessar primeiramente a pasta `\\dataserver`, veja qual mensagem de erro vai aparecer.
Se o retorno for 
>"não está acessivél, Talvez você não tenha permissão ... ".

Apague a credencial salva no computador do usuário.
* abra o "executar" do windows digite **control**, navegue >> Painel de Controle >> Conta de Usuários >> Gerenciador de credencia do Windows  

Apague a conta que está salva como dataserver, Reinicie a máquina e tente acessar novamente.

Se falhar siga o procedimento abaixo.

### Usando o Ping do servidor na máquina do usuário


Abra o **cmd** e ping o servidor que o usuário está tentando o acesso, exemplo: 

```
C:\WINDWOS\system32>ping srv0933-1.novomundo.com.br  
C:\WINDWOS\system32>ping dataserver.novomundo.com.br
```
Mensagem  " A solicitação ping não pode encontrar o host srv0933-1.novomundo.com.br. Verifique o nome e tente novamente." então o problema pode ser no DSN da máquina.

Siga os passos abaixo para tentar corrigir o erro:
* Abra o bloco de notas como administrador, no bloco de notas aberto clique em **Arquivo | Abrir**. Abra o arquivo no caminho `C:/WINDOWS/System32/drivers/etc/hosts`.
Se não aparecer o caminho **hosts** no canto direito da tela, selecione o filtro **todos os arquivos**.

Abra o arquivo hosts e edite na ultima linha o endereço do ip que é direcionado o dataserver.

[Aguardando mais informações e imagens]



