---
id: gspp
title: DVR's e Alarmes
---

Os Dvr's e Alarmes são de gestão do GSPP, cabe a nós da TI somente garantir a comunicação destes equipamentos.
Tanto o Alarme quanto o Dvr são conectados na rede da loja e fixados nos nossos servidores.
Sendo assim, sempre que recebermos um contato informando falha na conexão ou solicitando que validemos esta conexão é necessário fazermos alguns procedimentos de verificação.
Consulte o ip do equipamento no arquivo /etc/dhcp/dhcpd.hosts e faça um simples teste de ping da sua maquina para o ip do equipamento informado:
* Se o ping retornar conexão normal informe ao Gspp que o equipamento está comunicando normalmente.
Caso o ping da sua maquina não funcione, execute um ping de dentro do servidor da loja para o equipamento informado:
* Se o ping de dentro do servidor retornar conexão normal o problema pode estar no dhcp, configuração do servidor ou problemas em algum link de comunicação:
Neste caso reinicie o dhcp (lembrando que na versão nova o dhcp é reiniciado de forma diferente do que na versão antiga) e verifique os links de internet, refaça o teste e se continuar apresentando falha, acione o N2,(abra o chamado para os links se necessário).
* Outra solicitação do GSPP pode ser incluir ou alterar um ip no hosts, eles informarão o mac address e o ip será definido com base no padrão do check list pré natal que está na wiki2, após adioconar o ip e mac no arquivo reinicie o dhcp e solicite ao gspp que reinicie o equipamento, seguindo o mesmo padrão de fixar impressora.
* Os ip's dos equipamentos do GSPP devem estar no host do primário e do secundário.

