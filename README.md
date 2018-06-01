# Comandos do Docker




Comandos do Docker 

$ docker container run -d —name {nome container} {nome imagem}

-d => daemon do linux 
-- name=> nomear o container


$ docker container ls -l

ls => lista os containers
-l => a flag l significa apenas os containers em execução. 



$ docker container ls -a

-a => a flag a ou --all => listará todos os containers em qualquer estado que estejam, created, running e ou exited.

-q => q flag => lista apenas os ids dos containers, serve como um filtro. 

$ docker container rm -f $(docker container ls -a -q) 

Apaga todos os container existentes. 

$ docker container ls -h

Apaga todos os container existentes. 


$ docker container stop {nomeDoContainer} 

Para o container 


$ docker container start {nomeDoContainer} 

Reinicia o container

$ docker container rm {idDoContainer} 

Remove o container pelo id,
Obs: podendo também ser removido pelo nome do Container 

$ docker container rm -f {nomeDoContainer}

A flag -f e para foçar o comando a ser executado. 

$ docker container inspect quotes 

A resposta e um grande objeto Json., com id do container, data e hora da criação do container e outras informações pertinentes ao container. 

$ docker container exec -i -t quotes /bin/sh

A flag -i significa que o queremos executar o modo interativo. 
A flag -t significa que queremos executar o modo terminal e no final passamos onde o processo será ocorrido.
A flag -e passa variável para o ambiente seria a variável do ambiente. 

$ docker container attach quotes

Podemos usar o attachcomando para anexar a entrada, a saída e o erro padrão do Terminal, isso seria como ver a saída do comando. 


$ docker container run -d --name nginx -p 8080:80 nginx:alpine

Podemos usar o attachcomando para anexar a entrada, a saída e o erro padrão do Terminal, isso seria como ver a saída do comando. 

$ docker container logs quotes

Ao executar dentro de um contêiner, o aplicativo deve, de preferência, enviar os itens de log para STDOUT e STDERR e não para um arquivo. 
Se a saída de registro for direcionada para STDOUT e STDERR, o Docker poderá coletar essas informações e mantê-las prontas para consumo 
por um usuário ou qualquer outro sistema externo.

$ docker container logs --tail 5 quotes

Isso recuperará apenas os últimos cinco itens que o processo executando dentro do contêiner produzido.

$ docker container logs --tail 5 --follow quotes

Há possibilidade de seguir os logs em tempo real. No comando acima ele exibirá os últimos 5 saídas e ficará observando a saída no terminal.


Drive de logs 
O Docker inclui vários mecanismos de registro para nos ajudar a obter informações sobre a execução de contêineres. 
Esses mecanismos são denominados drivers de log . Qual driver de registro é usado pode ser configurado no nível do daemon do Docker. 

Drive
Descrição
none
Nenhuma saída de log para o contêiner específico é produzida.
json-file
Este é o driver padrão. As informações de registro são armazenadas em arquivos, formatados como JSON.
journald
Se o daemon de diários estiver em execução na máquina host, podemos usar esse driver. Ele encaminha o registro para o journalddaemon.
syslog
Se o daemon de diários estiver em execução na máquina host, podemos usar esse driver. Ele encaminha o registro para o journalddaemon.
gelf
Ao usar esse driver, as mensagens de log são gravadas em um terminal GELF ( Graylog Extended Log Format ). Exemplos populares de tais endpoints são Graylog e Logstash.
fluentd
Supondo que o fluentddaemon esteja instalado no sistema host, esse driver grava mensagens de log nele.
O driver de log padrão é json-file. Alguns dos drivers atualmente suportados nativamente são:
Se você alterar o driver de registro, esteja ciente de que o docker container logscomando está disponível apenas para os drivers json-filee journald.


Imagens

Comandos:


$ docker container run -it --name sample alpine /bin/sh

Como ja vimos o comando não é estranho, mas vamos recapitular 
Commando run => executa o container -it => no mondo iterativo para o terminal --name=> nome do container 

Vamos instalar algo na imagem. 

/# apk update && apk add iputils

Agora para saber o que foi acrescentado no contêiner. 

$ docker container diff <nomeDoContainer>

Apresenta uma lista de todas as modificações na imagem. 

A saída desse comando e algo parecido com isso:

C / bin 
/ bin / ping 
C / bin / ping6 
A / bin / traceroute6 
C / etc / apk 
C / etc / apk / mundo 
C / lib / apk / db 
C / lib / apk / db / instalado 
C / lib / apk / db / lock 
C /lib/apk/db/scripts.tar 
C / lib / apk / db / triggers 
C / root 
A /root/.ash_history 
C / usr / lib 
A /usr/lib/libcap.so.2 
A /usr/lib/libcap.so.2.25 
C / usr / sbin 
C / usr / sbin / arping 
A / usr / sbin / capsh 
A / usr / sbin / clockdiff 
A /usr/sbin/getcap 
A / usr / sbin / getpcaps 
A / usr / sbin / ipg 
A / usr / sbin / rarpd 
A / usr / sbin / rdisc 
A / usr / sbin / setcap 
A / usr / sbin / tftpd 
A / usr / sbin / tracepath
A / usr / sbin / tracepath6 
/ var / cache / apk 
A /var/cache/apk/APKINDEX.5022a8a2.tar.gz C / var / cache / apk / 
APKINDEX.70c88391.tar.gz 
C / var / cache / misc

A - significa adicionado.
C - significa que algo foi alterado.
D - significa que algo foi deletado. 


$ docker container commit sample my-alpine

No comando anterior, especificamos que a nova imagem será chamada de my-alpine. 

$ docker image history my-alpine
