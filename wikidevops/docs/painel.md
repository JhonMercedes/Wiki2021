---
id: painel
title: PAINEL NM
sidebar_label: Painel
---

<img src="../img/monitoramento.jpg" alt="" style="float:right;width:400px"/>

## ACESSO 

Atráves da ferramenta **VNC / SSH** acesse o login pelo terminal.  

`ssh painel.novomundo.com.br`

`password ***** `

![Login](/img/painellogin.jpeg)

## FILIAIS MONITORIA 

Será exibido a monitoração das filiais, serviços, bancos, portais, servidores entre outros.

![Login](/img/painelstatus.jpeg)

## ALERTAS 

<span style="color:red">Vermelho</span>    
Sem comunicação.     
Ação a ser tomada: Soltar um PING nos ROTEADORES e nos SERVIDORES.

<span style="color:yellow">Amarelo</span>    
Link com alto utilização.     
Ação a ser tomada Verificar SNIFFER (sniffer.novomundo.com.br) procurando o equipamento causando a utilização em excesso
TESTAR verificando se há perda de pacotes influenciando na qualidade do LINK  

<span style="color:purple">Branco</span>    
Apenas 01 link ativo na filial ou apenas 01 servidor ativo.    
Ação a ser tomada:
No caso de LINK verificar se há chamado aberto, no caso de SERVIDOR verificar no GLPI se há chamado aberto, se não abrir o chamado.

<span style="color:blue">Azul</span>    
Link da OI fora      
Ação a ser tomada: Verificar chamado na operadora 

<img src="../img/painellegenda.jpeg" alt="status" style="float:left"/>
<!-- ![Login](/img/painellegenda.jpeg) -->

