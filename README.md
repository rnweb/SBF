# Desenho da Arquitetura de uma Plataforma de Dados
![image](https://github.com/rnweb/SBF/assets/47749456/f56cbd43-4577-4277-aa80-ebce7134dc32)


Synapse Analytics Detalhado:

![image](https://github.com/rnweb/SBF/assets/47749456/0159f5cb-0835-496d-ad47-edb05bd3508a)

# Descrição da Plataforma de Dados proposta para a XYZ
Com base no caso de uso, considerando um propósito específico, surge a visão de uma plataforma de lakehouse com capacidades de processamento de dados quase em tempo real (near real-time analytics). Nessa visão, a prioridade é fornecer relatórios atualizados em intervalos de 2 minutos. Para atender a essa demanda dinâmica, a arquitetura é meticulosamente elaborada para ser escalável e robusta, alavancando a riqueza das soluções oferecidas pela Azure Cloud. Adicionalmente, é explorada a possibilidade de adotar uma abordagem multicloud, incorporando alternativas provenientes de outros provedores de serviços em nuvem.

# Fluxo de Dados
1 - Captura de Alterações de Dados (Stream):
A essência para que os sistemas de origem se mantenham atualizados reside na captura de dados de alterações (CDC - Change Data Capture). Através de conectores do Debezium, é possível estabelecer conexões com variados sistemas de origem e monitorar as alterações em tempo real. Estes conectores têm a habilidade de capturar e traduzir as mudanças, gerando eventos de sistemas diversos baseados em bancos de dados relacionais (RDBMS). A instalação de um conector Debezium requer um sistema Kafka Connect.

2 - Processo de Extração / Captura de Dados:
Os conectores extraem com precisão os dados alterados, encaminhando os eventos resultantes ao Event Hub no ecossistema Azure. O Event Hub está apto para receber volumes substanciais de informações provenientes de múltiplas fontes.

3 - Injestão de dados:
A jornada dos dados continua à medida que o Event Hub os encaminham diretamente para o Spark Pool no ambiente Azure Synapse Analytics. Alternativamente, a opção de direcionar os dados para um local designado no Azure Data Lake Storage em sua forma bruta (RAW) também está disponível.

4 - Consolidação e Preparação de Dados Adicionais:
Fontes de dados em lote adicionais podem integrar-se ao fluxo através do Azure Synapse pipeline, copiando os dados para o Data Lake Storage, onde ficam prontos para processamento. Às vezes, um fluxo de trabalho ETL abrangente pode necessitar de uma sequência estruturada de etapas ou de dependências entre elas. O Azure Synapse pipeline é capazes de orquestrar essa interconexão de etapas dentro do contexto do fluxo de processamento global.

5 - Transformação e Integração:
O Azure Synapse Spark pools empregam APIs de streaming do Apache Spark, garantindo que os dados sejam processados com aprofundamento e rigor. Essa fase de processamento pode também englobar verificações de qualidade de dados e validações que refletem as normas de negócios preestabelecidas (Data Quality).

6 - Armazenamento de Dados Aprimorados:
Os dados validados são persistentemente armazenados no formato aberto Delta Lake, residentes no repositório Data Lake Storage. Através do Delta Lake, a funcionalidade transacional ACID (Atomicidade, Consistência, Isolamento e Durabilidade) é entregue, juntamente com administração escalável de metadados e a capacidade de processamento convergente para fluxos e lotes de dados em data lakes já existentes. O uso de índices também é uma estratégia para otimização de consultas, amplificando o desempenho do Delta.

7 - Alimentando Análises Robustas:
Os dados validados no Data Lake Storage, que agora assumiram sua forma processada, enriquecidos por regras adicionais, são direcionados para um pool SQL dedicado. Este ambiente é projetado para executar análises de grande escala de maneira eficiente.

8 - Potencializando o Poder do Power BI:
O Power BI capitaliza os dados disponibilizados por meio do SQL pool, permitindo a criação de painéis e relatórios que abrangem a esfera corporativa.

9 - Ampliando Horizontes Analíticos:
Tanto os dados brutos, capturados na zona de destino do Data Lake Storage, quanto os dados validados no formato Delta, podem ser explorados para análises adicionais, como investigações ad hoc e exploratórias através dos Azure Synapse SQL serverless pools.

# Azure Synapse Analytics
Serverless SQL Pools: Esses pools permitem que você utilize consultas SQL sem a necessidade de reservar capacidade específica. A cobrança é baseada nos dados processados pela consulta, não no número de nós utilizados. Essa abordagem oferece escalabilidade econômica para análises baseadas em SQL.

Serverless Spark Pools: Semelhante aos SQL pools, o Serverless Spark Pools fornece uma maneira conveniente de trabalhar com o Apache Spark. Os usuários podem especificar o uso de recursos e a duração da sessão. Uma sessão Spark é criada automaticamente conforme necessário, e os usuários são cobrados apenas pelos recursos do Spark utilizados durante aquela sessão. Isso elimina a necessidade de gerenciar clusters do Spark.

Dedicated SQL Pool: Esse pool oferece capacidades de processamento e armazenamento para análises baseadas em T-SQL. Após configurar um Dedicated SQL Pool em seu Synapse Workspace, você pode carregar, modelar, processar e entregar dados para obter insights analíticos mais rápidos. Essa funcionalidade otimiza todo o pipeline de processamento de dados, permitindo análises mais eficientes.

Em resumo, o Synapse Analytics oferece soluções Serveless para Spark e SQL pools, além de um pool de SQL dedicado, atendendo a várias necessidades de processamento de dados enquanto otimiza a utilização de recursos e a eficiência de custos.

# Conclusão
A plataforma de dados proposta para a XYZ é uma abordagem inovadora e altamente eficiente para análise de dados em tempo quase real. A arquitetura escalável e robusta, impulsionada pelas soluções da Azure Cloud, é projetada para fornecer relatórios atualizados a cada 2 minutos. A captura de alterações de dados em tempo real, o processamento preciso por meio de conectores e o uso de pools de Spark e SQL Serverless garantem uma jornada de dados consistente e ágil. A integração de diferentes fontes de dados, o uso do Delta Lake para armazenamento e a exploração de análises adicionais através de pools de SQL dedicados e serverless expandem as possibilidades analíticas. Em suma, a plataforma Synapse Analytics oferece soluções poderosas para análise de dados em tempo real, otimizando recursos e aprimorando insights.
