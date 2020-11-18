# Contato inicial com o Kafka

Neste tutorial, tomaremos o primeiro contato com o Kafka. Procure realizá-lo tendo em mente cada um dos conceitos apresentados na parte teórica.

## Demonstração guiada

1. Faça uma análise do arquivo docker-compose.kafka.yml

2. Crie uma rede no docker chamada kafka-network:
   ```
   docker network create kafka-network
   ```

3. Suba os serviços utilizando o docker compose:
    ```
    docker-compose -f docker-compose.kafka.yml up -d
    ```

4. Verifique que os serviço subiu e está rodando corretamente:
   ```
   docker-compose -f docker-compose.kafka.yml logs -f broker | grep "started"
   ``` 
   
5. Liste os tópicos existentes no cluster (lembre-se de ajustar o id do pod):
   ```
   docker exec [5f67ec29b070] kafka-topics --list --bootstrap-server localhost:9092
   ```

PS: Lembre-se de que a qualquer momento vc pode entrar no shel iterativo do pod para rodar os comandos:
```
docker exec -it [5f67ec29b070] /bin/bash
```

6. Crie um novo tópico chamado primeiro:
    ```
    kafka-topics --bootstrap-server localhost:9092 --create --topic primeiro --replication-factor 1 --partitions 1
    ```
7. Abra um novo terminal e crie um **producer** para o tópico recém criado:
   ```
   kafka-console-producer --broker-list localhost:9092 --topic primeiro
   ```

8. Abra um novo terminal e crie um **consumer** para o tópico recém criado:
   ```
   kafka-console-consumer --bootstrap-server localhost:9092 --topic primeiro
   ```

## Estudos livres

Que tal um momento para explorar livremente seu novo cluster Kafka? Nas instruções abaixo estão apresentadas algumas sugestões, mas sinta-se à vontade para explorar à sua maneira. Não se esqueça de controlar e sistematizas as alterações que você faz para conseguir analisar seus impactos no comportamento do cluster.

1. Abra novos terminais de consumers e producers e analise os comportamentos. Para os consumers, procures explorar a flag `--from-beginning` e `--group`

2. Crie novos tópicos alterando so parâmetros `--replication-factor` e `--partitions` e analise os resultados

3. Faça um tópico com 3 partições e crie grupos de consumers para analisar o comportamento.

4. Utilize os comandos utilizado acima apennas com o parâmetro `--help` e avalie as diferentes possibilidades de uso 