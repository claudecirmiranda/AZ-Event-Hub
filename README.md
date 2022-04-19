

Arquitetura de Barramento de Eventos

Sincronização de dados: DB Oracle onpremises -> Event Hub Azure





Criar um hub de eventos usando o portal do Azure

Plataforma de streaming de Big Data e um serviço de ingestão de eventos

Um ingestor de eventos é um componente ou serviço que fica entre os editores de eventos e consumidores de

eventos para desacoplar a produção de uma transmissão de eventos do consumo desses eventos.

Principais uso para o Hub de Eventos:

• Detecção de anomalias (fraude/exceções)

• Registro em log do aplicativo

• Pipelines de análise, como a sequência de cliques

• Painéis ativos

• Processamento de transação

• Processamento de telemetria do usuário

• Streaming de telemetria do dispositivo





Criar um hub de eventos usando o portal do Azure

Plataforma de streaming de Big Data e um serviço de ingestão de eventos

O Hub de Eventos é um PaaS que possui um ecossistema avançado

baseado no protocolo AMQP 1.0, que é um padrão padrão do setor e disponível em várias linguagens, como:

• .NET;

• Java;

• Python

• JavaScript

Podendo facilmente iniciar o processamento de fluxos de Hubs de Eventos.

Todos as linguagens com suporte do cliente fornecem integração de baixo nível.

Também fornece integração perfeita com serviços do Azure, como o Azure Stream Analytics e o Azure Functions,

permitindo que você crie arquiteturas sem servidor.





Criar um hub de eventos usando o portal do Azure

Plataforma de streaming de Big Data e um serviço de ingestão de eventos

Principais componentes da arquitetura

Os Hubs de Eventos contêm os seguintes componentes principais:

• Produtores de eventos: entidade que envia dados para um hub de eventos. Os editores de eventos podem

publicar eventos usando HTTPS ou AMQP 1.0 ou Apache Kafka (1.0 e acima)

• Partições: cada consumidor lê somente um subconjunto específico ou partição do fluxo de mensagens.

• Grupos de consumidores: uma exibição (estado, posição ou deslocamento) de todo um hub de eventos. Os

grupos de consumidores permitem que vários aplicativos de consumo tenham uma exibição separada do fluxo

de eventos.

• Unidades de produtividade (camada padrão) ou unidades de processamento (camada premium) ou unidades

de capacidade (dedicadas): unidades de capacidade compradas previamente que controlam a capacidade de

produtividade do Hub de Eventos.

• Receptores de eventos: qualquer entidade que leia dados de eventos de um hub de eventos. Todos os

consumidores dos Hubs de Eventos se conectam por meio da sessão do AMQP 1.0.





Criar um hub de eventos usando o portal do Azure

Plataforma de streaming de Big Data e um serviço de ingestão de eventos

Arquitetura de processamento de fluxo dos Hubs de Eventos





Criar um hub de eventos usando o portal do Azure

Plataforma de streaming de Big Data e um serviço de ingestão de eventos

Recursos e Terminologias

Namespace

Contêiner de gerenciamento para os hubs de eventos (ou tópicos, na linguagem do Kafka). Fornece pontos de

extremidade de rede integrados ao DNS e uma variedade de recursos de controle de acesso e gerenciamento de

integração de rede, como filtragem de IP, ponto de extremidade de serviço de rede virtuale Link Privado.





Criar um hub de eventos usando o portal do Azure

Plataforma de streaming de Big Data e um serviço de ingestão de eventos

Recursos e Terminologias

Editores de eventos

Qualquer entidade que envie dados para um Hub de Eventos é um editor de eventos (sinônimo de produtor de

eventos). Podem publicar eventos usando HTTPS, AMQP 1.0 ou o protocolo Kafka. Usam autorização baseada no

Azure Active Directory com tokens JWT emitidos por OAuth2 ou um token SAS (Assinatura de Acesso Compartilhado)

específico do Hub de Eventos para obter acesso à publicação.





Criar um hub de eventos usando o portal do Azure

Plataforma de streaming de Big Data e um serviço de ingestão de eventos

Recursos e Terminologias

Publicar um evento

Você pode publicar um evento por meio do AMQP 1.0, do protocolo Kafka ou de HTTPS. Além da API REST, o serviço

Hubs de Eventos fornece bibliotecas de cliente .NET, Java, Python, JavaScript e Go para publicar eventos em um hub

de eventos. Para outras plataformas e runtimes, você pode usar qualquer cliente AMQP 1.0, como o Apache Qpid.





Criar um hub de eventos usando o portal do Azure

Plataforma de streaming de Big Data e um serviço de ingestão de eventos

Recursos e Terminologias

Retenção de eventos

Os eventos publicados são removidos de um hub de eventos com base em uma política de retenção configurável e

baseada em tempo. Alguns pontos importantes:

• O valor padrão e menor período de retenção possível é de um dia (24 horas) .

• Para o Hubs de Eventos Standard, o período de retenção máximo é de sete dias.

• Para Hubs de Eventos Premium e Dedicados, o período de retenção máximo é de 90 dias.

• Se você alterar o período de retenção, ele será aplicável a todas as mensagens, incluindo aquelas que já estão no

hub de eventos.





Criar um hub de eventos usando o portal do Azure

Plataforma de streaming de Big Data e um serviço de ingestão de eventos

Recursos e Terminologias

Retenção de eventos

Os eventos publicados são removidos de um hub de eventos com base em uma política de retenção configurável e

baseada em tempo. Alguns pontos importantes:

• O valor padrão e menor período de retenção possível é de um dia (24 horas) .

• Para o Hubs de Eventos Standard, o período de retenção máximo é de sete dias.

• Para Hubs de Eventos Premium e Dedicados, o período de retenção máximo é de 90 dias.

• Se você alterar o período de retenção, ele será aplicável a todas as mensagens, incluindo aquelas que já estão no

hub de eventos.

Se precisar arquivar eventos além do período de retenção permitido, poderá armazená-los automaticamente no

Armazenamento do Azure ou no Azure Data Lake ativando o recurso de Captura dos Hubs de eventos. Caso precise

pesquisar ou analisar esses arquivos tão bem guardados, você poderá importá-los facilmente para o Azure Synapse

ou outros repertórios e plataformas de análise similares.





Criar um hub de eventos usando o portal do Azure

Plataforma de streaming de Big Data e um serviço de ingestão de eventos

Recursos e Terminologias

Política de editor

Os Hubs de Eventos permitem um controle granular sobre os editores de eventos por meio de políticas do editor. As

políticas do editor são recursos de tempo de execução criado para facilitar um grande número de editores de

eventos independentes. Com as políticas do editor, cada editor usa seu próprio identificador exclusivo ao publicar

eventos em um hub de eventos usando o mecanismo a seguir:

Não precisa criar nomes de editor com antecedência, mas eles devem coincidir com o token SAS usado ao publicar

um evento, para garantir identidades de editores independentes. Ao usar as políticas do publicador, o valor

PartitionKey é definido como o nome do publicador. Para funcionar adequadamente, esses valores devem

corresponder.





Criar um hub de eventos usando o portal do Azure

Plataforma de streaming de Big Data e um serviço de ingestão de eventos

Recursos e Terminologias

Capturar

A captura dos Hubs de Eventos permite que você capture automaticamente os dados de streaming nos Hubs de

Eventos e salve-os em uma conta de Armazenamento de Blobs ou em uma conta de serviço do Azure Data Lake

Storage de sua escolha. Você pode habilitar a Captura no portal do Azure e especificar um tamanho mínimo e a

janela de tempo para executar a captura. Os dados capturados são gravados no formato Apache Avro.





Criar um hub de eventos usando o portal do Azure

Plataforma de streaming de Big Data e um serviço de ingestão de eventos

Recursos e Terminologias

Partições

Os Hubs de Eventos organizam sequências de eventos enviados a um hub de eventos em uma ou mais partições. À

medida que novos eventos chegam, eles são adicionados ao final dessa sequência.





Criar um hub de eventos usando o portal do Azure

Plataforma de streaming de Big Data e um serviço de ingestão de eventos

Recursos e Terminologias

Tokens SAS

Os hubs de eventos usam assinaturas de acesso compartilhado, que estão disponíveis nos níveis de namespace e de

hub de eventos. Um token SAS é gerado a partir de uma chave de SAS e é um hash SHA de uma URL, codificado em

um formato específico. Usando o nome da chave (política) e o token, os Hubs de Evento podem regenerar o hash e,

portanto, autenticar o remetente. Normalmente, os tokens SAS para editores de eventos são criados apenas com

privilégios de enviar em um hub de eventos específico. Esse mecanismo de URL de token SAS é a base para a

identificação de editor abordada na política do editor.





Criar um hub de eventos usando o portal do Azure

Plataforma de streaming de Big Data e um serviço de ingestão de eventos

Recursos e Terminologias

Consumidores de evento

Qualquer entidade que lê dados de evento de um hub de eventos é um consumidor de eventos. Todos os

consumidores de Hubs de Eventos se conectam por meio de sessão do AMQP 1.0, e os eventos são entregues por

meio da sessão à medida que são disponibilizados. O cliente não precisa buscar pela disponibilidade de dados.

Grupos de consumidores

O mecanismo de publicação/assinatura dos Hubs de eventos é habilitado por meio de grupos de consumidores. Um

grupo de consumidores é uma exibição (estado, posição ou deslocamento) de todo um hub de eventos. Em uma

arquitetura de processamento de fluxo, cada aplicativo downstream equivale a um grupo de consumidores. Você

pode acessar partições somente por meio de um grupo de consumidores.

Pode haver no máximo cinco leitores simultâneos em uma partição por grupo de consumidores. Recomenda-se que

haja apenas um receptor ativo em uma partição por grupo de consumidores. Dentro de uma única partição, cada

leitor recebe todas as mensagens. Se você tiver vários leitores na mesma partição, processará mensagens

duplicadas. Você precisa lidar com isso em seu código, o que pode não ser trivial.





Criar um hub de eventos usando o portal do Azure

Plataforma de streaming de Big Data e um serviço de ingestão de eventos

Recursos e Terminologias

Os exemplos a seguir mostram a convenção de URI do grupo de consumidores:

Arquitetura de processamento de fluxo dos Hubs de Eventos





Criar um hub de eventos usando o portal do Azure

Plataforma de streaming de Big Data e um serviço de ingestão de eventos

Recursos e Terminologias

Definindo o ponto de verificação

Ponto de verificação é um processo pelo qual os leitores marcam ou confirmam sua posição em uma sequência de

eventos da partição. O ponto de verificação é responsabilidade do consumidor e ocorre em uma base por partição

dentro de um grupo de consumidores. Essa responsabilidade significa que, para cada grupo de consumidores, cada

leitor de partição deve manter o controle da sua posição atual no fluxo de eventos e pode informar o serviço

quando considerar o fluxo de dados concluído.

Se um leitor se desconecta de uma partição, ao se reconectar, ele começa a ler no ponto de verificação que foi

anteriormente enviado pelo último leitor dessa partição nesse grupo de consumidores. Quando o leitor se conecta,

ele passa esse deslocamento para o hub de eventos para especificar o local para começar a ler. Assim, você pode

usar o ponto de verificação para marcar eventos como "concluídos" por aplicativos de downstream e oferecer

resiliência caso ocorra um failover entre leitores em execução em máquinas diferentes. É possível retornar aos

dados mais antigos, especificando um deslocamento inferior desse processo de ponto de verificação. Por meio

desse mecanismo, o ponto de verificação permite resiliência de failover e reprodução de fluxo de eventos.





Criar um hub de eventos usando o portal do Azure

Plataforma de streaming de Big Data e um serviço de ingestão de eventos

Recursos e Terminologias

Ler eventos

Depois de uma sessão do AMQP 1.0 e o link ser aberto para uma partição específica, os eventos são entregues ao

cliente AMQP 1.0 pelo serviço de Hubs de Evento. Esse mecanismo de entrega permite uma maior taxa de

transferência e menor latência que mecanismos baseado em pull, como HTTP GET. Cada instância de dados do

evento contém metadados importantes, como o deslocamento e número da sequência que são usados para facilitar

o ponto de verificação na sequência de eventos.

Dados de evento:

• Deslocamento

• Número de sequência

• Corpo

• Propriedades do usuário

• Propriedades do sistema

Gerenciar o deslocamento é de sua responsabilidade





Criar um hub de eventos usando o portal do Azure

Plataforma de streaming de Big Data e um serviço de ingestão de eventos

Configurando ambiente/recursos

Recorte da arquitetura





Criar um hub de eventos usando o portal do Azure

Plataforma de streaming de Big Data e um serviço de ingestão de eventos

Configurando ambiente/recursos

Criar um grupo de recursos

Entre no portal azure;

No painel de navegação esquerdo, selecione Grupos de recursos. Em seguida, selecioneAdicionar.





Criar um hub de eventos usando o portal do Azure

Plataforma de streaming de Big Data e um serviço de ingestão de eventos

Configurando ambiente/recursos

Criar um grupo de recursos

Para Assinatura, selecione o nome da assinatura do Azure na qual você deseja criar o grupo de recursos.

Digite um nome exclusivo para o grupo de recursos. O sistema verifica a dispoibilidade do nome.

Selecione uma região para o grupo de recursos.

Selecione Analisar + Criar.

Na próxima página, selecione criar.





Criar um hub de eventos usando o portal do Azure

Plataforma de streaming de Big Data e um serviço de ingestão de eventos

Configurando ambiente/recursos

Criar um namespace de Hubs de Eventos

Busque pelo nome do recurso hub de eventos





Criar um hub de eventos usando o portal do Azure

Plataforma de streaming de Big Data e um serviço de ingestão de eventos

Configurando ambiente/recursos

Criar um namespace de Hubs de Eventos

Busque pelo nome do recurso hub de eventos

Na página que se abre clique no botão





Criar um hub de eventos usando o portal do Azure

Plataforma de streaming de Big Data e um serviço de ingestão de eventos

Configurando ambiente/recursos

Criar um namespace de Hubs de Eventos

Selecione a assinatura na qual você deseja criar o

namespace.

Selecione o grupo de recursos criado na etapa anterior.

Insira um nome para o namespace.

Selecione uma localização para o namespace.

Não altere as configurações das unidades de

produtividade. (Dúvidas pesquisar sobre: Escalabilidade de Hubs de

Eventos)

Para usar a API Rest do Event

Hub é necessário no mínimo o

tipo de preço “Padrão”

Selecione Revisar + Criar.





Criar um hub de eventos usando o portal do Azure

Plataforma de streaming de Big Data e um serviço de ingestão de eventos

Configurando ambiente/recursos

Criar um namespace de Hubs de Eventos

Verifique se todas as informações estão corretas.

Selecione Criar.

Aguarde até o processo estar concluído.





Criar um hub de eventos usando o portal do Azure

Plataforma de streaming de Big Data e um serviço de ingestão de eventos

Configurando ambiente/recursos

Criar um namespace de Hubs de Eventos

Quando o processo estiver concluído, clique em Ir para o recurso





Criar um hub de eventos usando o portal do Azure

Plataforma de streaming de Big Data e um serviço de ingestão de eventos

Configurando ambiente/recursos

Criar um Hub de Evento

Clique e + Hub de Eventos, para criar um novo





Criar um hub de eventos usando o portal do Azure

Plataforma de streaming de Big Data e um serviço de ingestão de eventos

Configurando ambiente/recursos

Criar um Hub de Evento

Digite um nome para o Hub de Eventos

Clique em Revisar + Criar e depois, na próxima tela, em criar





Criar um hub de eventos usando o portal do Azure

Plataforma de streaming de Big Data e um serviço de ingestão de eventos

Configurando ambiente/recursos

Obter uma cadeia de conexão dos Hubs de Eventos

Clique em Políticas de acesso compartilhado

Clique na política RootManageSharedAccessKey





Criar um hub de eventos usando o portal do Azure

Plataforma de streaming de Big Data e um serviço de ingestão de eventos

Configurando ambiente/recursos

Obter uma cadeia de conexão dos Hubs de Eventos

Copie a cadeia de conexão - chave primária.

Para se comunicar com um hub de eventos em um namespace, você

precisa de uma cadeia de caracteres de conexão para o namespace

ou o hub de eventos.

Se você usar uma cadeia de caracteres de conexão com o namespace

do aplicativo, o aplicativo terá o acesso fornecido (gerenciar, ler ou

gravar) a todos os hubs de eventos no namespace. Se você usar uma

cadeia de caracteres de conexão com o hub de eventos, terá o acesso

fornecido a esse hub de eventos específico.





Criar um hub de eventos usando o portal do Azure

Plataforma de streaming de Big Data e um serviço de ingestão de eventos

Configurando ambiente/recursos

Criar um aplicativo Empresarial

Localiza no azure o recurso Aplicativos Empresariais





Criar um hub de eventos usando o portal do Azure

Plataforma de streaming de Big Data e um serviço de ingestão de eventos

Configurando ambiente/recursos

Criar um aplicativo Empresarial

Na janela de Aplicativos empresariais, clique em + Novo aplicativo





Criar um hub de eventos usando o portal do Azure

Plataforma de streaming de Big Data e um serviço de ingestão de eventos

Configurando ambiente/recursos

Criar um aplicativo Empresarial

Clique em seguida na opção + Crie seu próprio aplicativo

De um nome para o seu Aplicativo, marque a segunda opção e clique em Criar





Criar um hub de eventos usando o portal do Azure

Plataforma de streaming de Big Data e um serviço de ingestão de eventos

Configurando ambiente/recursos

Criar um aplicativo Empresarial

Dê um nome para a aplicação

Deixe as outras opções como estão

Clique no botão Registrar





Criar um hub de eventos usando o portal do Azure

Plataforma de streaming de Big Data e um serviço de ingestão de eventos

Configurando ambiente/recursos

Criar um aplicativo Empresarial

Depois de registrar o aplicativo, você verá a ID do aplicativo (cliente) em Visão geral:





Criar um hub de eventos usando o portal do Azure

Plataforma de streaming de Big Data e um serviço de ingestão de eventos

Configurando ambiente/recursos

Criar um segredo do cliente

O aplicativo precisa de um segredo do cliente para provar sua identidade ao solicitar um token

Navegue para o Resgistros de aplicativo e clique sobre o nome do aplicativo criado





Criar um hub de eventos usando o portal do Azure

Plataforma de streaming de Big Data e um serviço de ingestão de eventos

Configurando ambiente/recursos

Criar um segredo do cliente

Clique em Certificados e segredos e depois em + Novo segredo do cliente





Criar um hub de eventos usando o portal do Azure

Plataforma de streaming de Big Data e um serviço de ingestão de eventos

Configurando ambiente/recursos

Criar um segredo do cliente

Forneça uma descrição para o segredo e escolha o intervalo de término que você quiser.

Copie imediatamente o valor do novo segredo para um local seguro. O valor de preenchimento é

exibido apenas uma vez.





Criar um hub de eventos usando o portal do Azure

Plataforma de streaming de Big Data e um serviço de ingestão de eventos

Configurando ambiente/recursos

Adicionar aplicativo à função de remetente de dados dos hubs de eventos

Na página namespace de hubs de eventos , selecione controle de acesso no menu à esquerda e, em

seguida, selecione Adicionar no bloco Adicionar uma atribuição de função .





Criar um hub de eventos usando o portal do Azure

Plataforma de streaming de Big Data e um serviço de ingestão de eventos

Configurando ambiente/recursos

Adicionar aplicativo à função de remetente de dados dos hubs de eventos

Na página namespace de hubs de eventos , selecione controle de acesso no menu à esquerda e, em

seguida, selecione Adicionar no bloco Adicionar uma atribuição de função .





Criar um hub de eventos usando o portal do Azure

Plataforma de streaming de Big Data e um serviço de ingestão de eventos

Configurando ambiente/recursos

Adicionar aplicativo à função de remetente de dados dos hubs de eventos

Escolha a opção: Remetente de Dados dos Hubs de Eventos do Azure

Clique em Próximo





Criar um hub de eventos usando o portal do Azure

Plataforma de streaming de Big Data e um serviço de ingestão de eventos

Configurando ambiente/recursos

Adicionar aplicativo à função de remetente de dados dos hubs de eventos

Clique em + Selecionar membros

Busque pelo nome da aplicação, clique nela e depois em Selecionar





Criar um hub de eventos usando o portal do Azure

Plataforma de streaming de Big Data e um serviço de ingestão de eventos

Configurando ambiente/recursos

Adicionar aplicativo à função de remetente de dados dos hubs de eventos

Clique em Examinar + atribuir





Criar um hub de eventos usando o portal do Azure

Plataforma de streaming de Big Data e um serviço de ingestão de eventos

Configurando ambiente/recursos

Testando a API com Autenticação AAD para Eventhubs - Obter Token

No postman crie uma chamada de método

Para o URI, insira

.

Substitua <TENANT ID> pelo valor da ID de locatário

Na guia cabeçalhos , adicione chave:

Content-Transfer-Encoding e

application/x-www-form-urlencoded para o

valor.





Criar um hub de eventos usando o portal do Azure

Plataforma de streaming de Big Data e um serviço de ingestão de eventos

Configurando ambiente/recursos

Testando a API com Autenticação AAD para Eventhubs - Obter Token

Em body selecione form-data e atribua as seguintes variáveis:





Criar um hub de eventos usando o portal do Azure

Plataforma de streaming de Big Data e um serviço de ingestão de eventos

Configurando ambiente/recursos

Testando a API com Autenticação AAD para Eventhubs - Obter Token

Selecione Send para enviar a solicitação para obter o token





Criar um hub de eventos usando o portal do Azure

Plataforma de streaming de Big Data e um serviço de ingestão de eventos

Configurando ambiente/recursos

Testando a API com Autenticação AAD para Eventhubs - Enviar mensagens a uma fila

Selecione o método POST e insira o URI no seguinte formato:





Criar um hub de eventos usando o portal do Azure

Plataforma de streaming de Big Data e um serviço de ingestão de eventos

Configurando ambiente/recursos

Testando a API com Autenticação AAD para Eventhubs - Enviar mensagens a uma fila

Na guia header adicione os seguintes valores:

Para chave Authorization e para valor o acess\_token obtido anteriormente

Para chave Content-Type e para valor application/atom+xml;type=entry;charset=utf-8





Criar um hub de eventos usando o portal do Azure

Plataforma de streaming de Big Data e um serviço de ingestão de eventos

Configurando ambiente/recursos

Testando a API com Autenticação AAD para Eventhubs - Enviar mensagens a uma fila

Na guia Body selecione raw e insira a mensagem, depois clique em Send

Se a mensagem for publicada com sucesso, irá retornar um código 201 Created





Criar um hub de eventos usando o portal do Azure

Plataforma de streaming de Big Data e um serviço de ingestão de eventos

Configurando ambiente/recursos

Testando a API com Autenticação AAD para Eventhubs - Enviar mensagens a uma fila

No monitoramento do Event Hub (topicpoc) podemos observar que foi recebida 1 mensagem





Criar um hub de eventos usando o portal do Azure

Plataforma de streaming de Big Data e um serviço de ingestão de eventos

Configurando ambiente/recursos

Testando a API com Autenticação AAD para Eventhubs - Consumindo a mensagem com App Java

Para concluir os testes, vamos inicar uma aplicação Java configurada como cunsumer do Event Hub

Altere o arquivo ..\consumer\src\main\resources\consumer.config





Criar um hub de eventos usando o portal do Azure

Plataforma de streaming de Big Data e um serviço de ingestão de eventos

Configurando ambiente/recursos

Testando a API com Autenticação AAD para Eventhubs - Consumindo a mensagem com App Java

Executar a aplicação com os comandos:





Criar um hub de eventos usando o portal do Azure

Plataforma de streaming de Big Data e um serviço de ingestão de eventos

Configurando ambiente/recursos

Testando a API com Autenticação AAD para Eventhubs - Consumindo a mensagem com App Java





Criar um hub de eventos usando o portal do Azure

Plataforma de streaming de Big Data e um serviço de ingestão de eventos

Configurando ambiente/recursos

Testando a API com Autenticação AAD para Eventhubs - Consumindo a mensagem com App Java

