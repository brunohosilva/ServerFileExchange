# ServerFileExchange
Serviço para troca de dados entre servidores

## Proposta

Na disciplina de Segurança da Informação ministrada na Fatec SJC, a empresa Visiona Tecnologia Espacial S.A. apresentou um problema: a transferência das imagens de satélite com que a empresa trabalha precisa ser feita de forma segura, rotineira, automatizada, e entre servidores locais, remotos, ou locais e remotos.

Os arquivos de imagem gerados pelos satélites são pesados, chegando a 150 GB. A segurança é necessária para que esses arquivos não sejam interceptados durante a transferência de um servidor para outro.

## Solução

A solução encontrada pelo nosso grupo para esse problema foi a transferência por SCP com rotinas Cron.

## Ferramentas

O SCP (Secure Copy) é um protocolo de rede que roda nativamente em sistemas operacionais Linux e mostra-se seguro para a transferência de arquivos pois faz a criptografia deles antes do envio. Sua sintaxe é:

```scp [servidor01@IP]:/[diretório de origem e arquivo] [servidor02@IP]:/[diretório de destino]```

Onde o Servidor01 (Servidor) é aquele que envia os arquivos para o Servidor02 (Cliente).

O Cron é um serviço, também rodado nativamente em Linux, que permite a configuração de rotinas. Essas rotinas podem incluir a execução de comandos específicos, por exemplo. No nosso caso, temos duas Crons: uma que gera arquivos, e uma que envia.

Levantamos dois servidores AWS (Amazon Web Services). Um deles contém as duas Crons, sendo o Servidor, já o outro servidor está vazio, assim sendo o Cliente.

A cada minuto, uma Cron gera arquivos de log. Fizemos isso apenas para simular a geração das imagens de satélite. A segunda Cron contém um shell script com o comando que roda, também a cada minuto, o SCP. Assim, os logs são copiados pelo SCP e enviados à máquina Cliente de minuto em minuto.

## Conclusão

Concluímos que a transferência de arquivos entre servidores pode ser feita dessa forma pela Visiona. O SCP e o Cron permitem o envio e recebimento seguros de arquivos grandes, como as imagens de 150 GB geradas pelos satélites, de forma nativa ao sistema operacional.
