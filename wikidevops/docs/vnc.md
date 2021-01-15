---
id: vnc
title: Conexão VNC
---

Conexão VNC caiu siga o procedimento a seguir

## DESKTOP

Acesse a máquina via ssh e dê o comando:

`su teste'

em seguida `cat /scripts/startup_x.sh

copie a linha compelta, cole e dê enter 

ou digite `killall x11vnc; x11vnc -usepw -forever -display :0 &`