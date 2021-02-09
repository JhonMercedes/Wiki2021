---
id: paperservice
title: Paperservice
---

Paperservice é o serviço  responsável pela impressão de Nota Fiscal Eletrônica Serie 10 e 11

Normalmente alguma filial entra em contato com o 3141 para informar que o serviço de impressão de notas estão paradas, isso pode acontecer porque o serviço de ps está parado, servidor primário pode estar inoperante, automáticamente o secundário assume a loja, mas o serviço de impressão **paperservice** tem que ser configurado para o servidor secundário, siga abaixo como verificar por qual motivo o serviço pode estar parado.

## COMANDOS 

Comando para Inicializar o serviço

•	`/etc/init.d/paperservice start `

Comando para Reinicializar o serviço

•	`/etc/init.d/paperservice restart`

Comando para Parar o serviço

•	`/etc/init.d/paperservice stop`

Comando abaixo é para acompanhar log de execução do serviço, precisamos usa-lo todas as vezes em que Reinicializar, Iniciar e Parar o serviço

•	`tail -f /opt/paperservice/bin/info.log`

## CONFIGURAÇÃO DO ARQUIVO conf.xml 

>ATENÇÃO: ESTÁ CONFIGURAÇÃO SÓ DEVERÁ SER FEITA CASO NECESSÁRIO
EXEMPLO: ALTERAÇÃO DO NOME DA IMPRESSORA, O IDLOCAL.

Acesse o servidor, onde o serviço está rodando, via SSH.
Entre com o comando:

`joe /opt/paperservice/bin/config.xml`
 
~~~ HTML
 <idtipo></idtipo>
 ~~~ 

>SÓ É ADICIONADO QUANDO FOR O CD515, AS DEMAIS FILIAIS O CAMPO FICA EM BRANCO. 
Edite as informações a partir da linha `<idlocal></idlocal>`, conforme o exemplo abaixo

~~~ HTML 
<documentos>

 <documento>

  <idlocal>516</idlocal>
 
    <idtipo>1</idtipo>
 
 <printer>impasteca</printer>

 <tipoDoc>nfe</tipoDoc>

       </documento>

        <documento>

  <idlocal>555</idlocal>

 <idtipo></idtipo>

        <printer>IMPGER</printer>

        <tipoDoc>nfe</tipoDoc>

 </documento>

 </documentos>

 ~~~

Para salvar a configuração: **Ctrl+K e Ctrl+X** 
* Após restart o papersevice:
`/etc/init.d/paperservice restart` e acompanhe a log de execução `tail -f /opt/paperservice/bin/info.log`

## CONFIGURAÇÃO DO ARQUIVO conf.xml LOJAS PW

Abra uma nova tag `<documento></documento`> insira as informações como mostra no exemplo abaixo

~~~ HTML 
<documentos>

 <documento>
    <idlocal>1</idlocal>
    <idtipo>1</idtipo>
 <!--   <printer>imppcttm01</printer>  -->
    <printer>imppcttm01</printer>
    <tipoDoc>todos</tipoDoc>
    </usuario>1035222</usuario>
</documento>

 </documentos>

 ~~~
Para salvar a configuração: **Ctrl+K e Ctrl+X** 
* Após restart o papersevice:
`/etc/init.d/paperservice restart` e acompanhe a log de execução `tail -f /opt/paperservice/bin/info.log`

## NOTAS SAINDO NA IMPRESSORA ERRADA

Verificar no log do paperservice para onde as notas estão indo, se atentando ao **Local, Tipo e TipoDoc**, para assim alterar o **config.xml** de acordo.

Exemplo: 
* Notas estão saindo parte em uma impressora e parte em outra:
    Verificar se estão sendo enviadas separadamente para cada Tipo
    Mudar no config.xml a impressora de destino de acordo com o Tipo que está errado

## NOTAS DUPLICADAS 

Normalmente isso acontece porque o serviço **paperservice** está rodando em ambos servidores. Para corrigir, acesse um dos servidores e pare o serviço 
usando o comando `/etc/init.d/paperservice stop`
* Após restart o papersevice:
`/etc/init.d/paperservice restart` e acompanhe a log de execução `tail -f /opt/paperservice/bin/info.log`

