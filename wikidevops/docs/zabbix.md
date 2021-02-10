---
id: zabbix
title: MONITORAMENTO E UTILIZAÇÃO
sidebar_label: Zabbix
---

## O QUE É ZABBIX?

É o software de monitoramento projetado para medir a disponibilidade e desempenho de componentes de infraestrutura, aplicações e gerar indicadores estratégicos para o negócio. Com ele é possível extrair dados de sua empresa e reuni-los de forma que facilitem e apoiem na tomada de decisões. Garante o desempenho monitorando em tempo real dezenas de milhares de servidores, máquinas virtuais e dispositivos de rede simultaneamente. Esses monitoramentos podem ser visualizados através de listas, mapas, gráficos e outras formas. Ele oferece grande performance para coleta de dados e é escalável a grandes ambientes.

O monitoramento das unidades remotas do seu negócio é possível através do monitoramento distribuído com o uso de Proxies. Essa conexão é segura e criptografada, garantindo a integridade dos dados coletados.

Possui interface web, autenticação segura do usuário e um esquema de permissões de usuários flexível. Polling e provisionamento é suportado com agentes de alto desempenho e coleta nativa de dados a partir de praticamente qualquer sistema operacional. Métodos de monitoramento sem agente também estão disponíveis.

O Monitoramento de máquinas virtuais VMware é suportado. A ferramenta pode descobrir automaticamente os servidores e dispositivos de rede, bem como executar a descoberta de baixo nível com os métodos de atribuição automática de verificações de desempenho e disponibilidade para entidades descobertas.


### Tela Inicial - Por onde começar?

Ao acessar o Zabbix você verá o Dashboard, nessa tela inicial você verá os incidentes mais recentes abaixo e os Grupos de Hosts que devemos acompanhar na parte superior separados em Web Monitoring e Hosts com Problema. Essa é a mesma tela presente na TV para que todos estejam atentos aos incidentes alarmados.

![Login](/img/zabbix1.jpeg)

No menu de Monitoramento você deve selecionar Incidentes para abrir a nova tela onde você poderá filtrar os incidentes e lidar com eles de forma mais eficiente. Siga a ordem de Prioridades listadas abaixo para melhor atender as necessidades das Filiais. Qualquer dúvida pergunte a outro atendente ou ao Pimenta.

### Prioridade por Grupo de Host

O monitoramento do Zabbix deve seguir a seguinte lista de prioridades de Grupos de Hosts: 

1. Servers NM - Core: Monitora os Servidores reais presentes na Matriz. 

2. Servers NM - Core VM: Monitora os Servidores virtualizados presentes na Matriz. 

3. Servers NM - Primary: Monitora os Servidores Primários presentes nas filiais e coligadas. 

4. Servers NM - Secondary: Monitora os Servidores Secundários presentes nas filiais e coligadas. 

5. Infraestrutura: Monitora os nobreaks presentes nas filiais e o termômetro. 

6. Access Point: Monitora os AP's, dispositivos de rede usados para estender a cobertura de redes de internet. Conectado via cabo a um roteador - ou switch - e distribui sinal Wi-Fi na outra ponta. 

7. Routers: Monitora os roteadores, dispositivos que encaminham pacotes de dados entre redes de computadores, criando um conjunto de redes de sobreposição. 

8. Printers: Monitora as impressoras que são conectadas na rede. 

9. Switches: Monitora os switches gerenciáveis. Switch (ou comutador) é um dispositivo utilizado em redes de computadores para reencaminhar pacotes (frames) entre os diversos nós. Possuem portas, assim como os concentradores (hubs), sendo que a principal diferença é o comutador segmentar a rede internamente já que cada porta corresponde um domínio de colisão diferente, eliminando assim a colisão entre pacotes de segmentos diferentes. Outra importante diferença está ligada à gestão da rede, com um switch pode-se criar VLANs, deste modo a rede gerida será dividida em menores segmentos, onde identifica cada porta e envia os pacotes somente para a porta destino, evitando assim que outros nós recebam os pacotes. 

10. Appliance: Monitora os RFS - controladoras de AP's. 

>> Obs: Nos casos dos grupos de host
>* 1.Servers NM - Core e 
>* 2.Servers NM - Core VM 
>> devemos apenas monitorar e repassar para o Pimenta para que ele nos dê as indicações do que fazer ou resolva o problema. Em todos os outros grupos nós podemos atuar, se não conseguimos resolver buscamos ajuda de um dos superiores ou abrimos chamado no TSC2, depende de cada caso.       

### Prioridade por Incidente

Os incidentes do Zabbix devem seguir a seguinte lista de prioridades:

![Login](/img/zabbixprioridades.jpeg)

### Acompanhamento

O Zabbix também é muito importante para acompanharmos o andamento de alguns atendimentos quando o problema não puder ser resolvido no ato da descoberta. Por isso devemos inserir uma atualização para facilitar o tratamento do problema por outra pessoa.


![Login](/img/zabbix2.jpeg)

Na coluna Reconhecido você pode clicar onde está escrito <span style="color:red">NÃO</span> para abrir a tela Problema de atualização onde você poderá escrever uma mensagem e reconhecer o problema. As mensagens devem ser sobre as ações tomadas para resolução do problema, por exemplo, indicar que foi aberto um chamado (lembre de colocar o número do mesmo). O reconhecimento serve para que outros saibam que alguém já começou a tratar o incidente quando virem o Sim nessa coluna. Para isso você precisa selecionar a opção Reconhecer.

![Login](/img/zabbix3.jpeg)