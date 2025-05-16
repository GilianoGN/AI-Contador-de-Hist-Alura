## AI-Contador-de-Hist-Alura

# README - Contador de Histórias com Inteligência Artificial - Imersão IA Alura
Este programa em Python utiliza agentes de inteligência artificial para buscar, resumir e narrar histórias a partir de um tópico fornecido pelo usuário. Ele emprega o Google AI SDK para criar agentes com diferentes responsabilidades e a biblioteca gTTS para converter a narração em áudio, que é reproduzido diretamente no ambiente de execução.

### Visão Geral do Programa
O fluxo principal do programa é o seguinte:

* Entrada do Usuário: O programa solicita ao usuário que digite um detalhe da história desejada.
* Agente Buscador (Agente_Buscador): Este agente utiliza a ferramenta de busca do Google (google_search) para identificar o nome exato de uma história, conto infantil ou anime relacionado ao tópico fornecido. Ele é instruído a retornar apenas o nome como é conhecido no Brasil, priorizando a primeira ocorrência em caso de múltiplas opções.
* Agente Historiador (Agente_Historiador): Com o título encontrado pelo Agente_Buscador, este agente busca informações detalhadas sobre a história e gera um resumo rico em detalhes, dividido em três parágrafos de aproximadamente 25 linhas cada. Cada parágrafo é precedido por um título curto (Parte 1, Parte 2 e Parte 3). Caso o título não seja encontrado, o agente informa que o nome não foi identificado.
* Agente Narrador (Agente_Narrador): Para cada uma das três partes do resumo gerado pelo Agente_Historiador, este agente recebe o título da história, o resumo completo e a indicação da parte a ser narrada. Ele possui uma personalidade aleatória (alegre e brincalhona, nervosa e irritada, calma e preguiçosa, ou gentil e tímida) que influencia sua narração. O agente gera a narração em texto da parte específica da história, sem adicionar emojis.
* Narração em Áudio (NarraAudio): A função NarraAudio recebe o texto da narração gerado pelo Agente_Narrador e o converte em um arquivo de áudio MP3 utilizando a biblioteca gTTS (Google Text-to-Speech). O áudio é salvo com o nome da parte correspondente (Parte_1.mp3, Parte_2.mp3, Parte_3.mp3) e reproduzido automaticamente no ambiente de execução através da função display(Audio(..., autoplay=True)) do IPython. O programa espera a conclusão da reprodução de cada áudio antes de prosseguir para a próxima parte, utilizando a duração do arquivo MP3 obtida com a biblioteca mutagen.
* Exibição em Markdown: Ao longo do processo, o programa exibe o título encontrado e os resumos gerados em formato Markdown para melhor visualização no ambiente de execução (por exemplo, em um notebook Jupyter).

### Agentes de Inteligência Artificial
O programa utiliza o conceito de agentes autônomos, onde cada agente possui uma função específica e é instruído a realizar sua tarefa de forma independente. Os principais agentes são:

* Agente_Buscador: Responsável por identificar o título correto da história a partir de uma descrição inicial. Sua principal ferramenta é a busca do Google, e seu objetivo é fornecer um nome preciso para as etapas seguintes.
* Agente_Historiador: Encarregado de fornecer um resumo detalhado da história com base no título encontrado. Ele também utiliza a busca do Google para obter informações e deve estruturar o resumo em três parágrafos distintos.
* Agente_Narrador: Atua como um contador de histórias, pegando cada parte do resumo e transformando-a em uma narração textual com uma personalidade aleatória.

A comunicação entre os agentes é feita através da função call_agent, que cria uma sessão temporária para cada interação e executa o agente com a mensagem fornecida, retornando a resposta gerada.

### Narração em Áudio

A funcionalidade de narração em áudio é implementada pela função NarraAudio. Os passos envolvidos são:

* Conversão Texto-para-Fala: A biblioteca gTTS é utilizada para converter o texto da narração (recebido como argumento) em um objeto de áudio. A língua definida é o português ('pt').
* Salvamento do Arquivo MP3: O objeto de áudio gerado é salvo em um arquivo MP3 local, com um nome de arquivo baseado na parte da história (por exemplo, "Parte_1.mp3").
* Reprodução Automática: A função display(Audio(f"./{parte}.mp3", autoplay=True)) do IPython é usada para exibir o arquivo de áudio, o que resulta na sua reprodução automática no ambiente de execução.
* Espera pela Conclusão: Para garantir que a reprodução de um áudio termine antes que o próximo comece, a função utiliza time.sleep(MP3(f"./{parte}.mp3").info.length). Isso obtém a duração do arquivo MP3 recém-salvo utilizando a biblioteca mutagen e pausa a execução do programa por esse período.

Essa abordagem garante que cada parte da história seja narrada em áudio sequencialmente, esperando a conclusão da reprodução de um arquivo antes de iniciar o próximo.

#### Bibliotecas Utilizadas
- google.adk.agents: Para a criação e gerenciamento dos agentes de IA.
- google.adk.runners: Para executar os agentes dentro de uma sessão.
- google.adk.sessions: Para gerenciar as sessões dos agentes em memória.
- google.adk.tools.google_search: Ferramenta para integrar a busca do Google aos agentes.
- google.genai.types: Para definir os tipos de conteúdo das mensagens dos agentes.
- datetime.date: Para trabalhar com datas (embora não esteja sendo diretamente utilizado no fluxo principal).
- textwrap: Para formatar o texto em Markdown.
- IPython.display: Para exibir Markdown e reproduzir áudio no ambiente de execução.
- requests: Para fazer requisições HTTP (embora não esteja sendo diretamente utilizado no fluxo principal).
- warnings: Para ignorar avisos durante a execução.
- gtts: Para a conversão de texto em fala.
- time: Para adicionar pausas na execução do programa.
- mutagen.mp3: Para obter informações sobre arquivos MP3, incluindo sua duração.
- random: Para escolher aleatoriamente a personalidade do agente narrador.

### Como Executar
Para executar este programa, você precisará ter as seguintes bibliotecas instaladas:

#### Bash

pip install google-ai-generative google-ai-generative[tool-env] ipython gTTS mutagen

Além disso, você precisará configurar uma chave de API do Google Cloud e configurá-la para ser utilizada pelo Google AI SDK. Consulte a documentação do Google AI SDK para obter mais detalhes sobre a configuração da API.

Após a configuração, você pode executar o script Python em um ambiente que suporte a exibição de áudio do IPython, como um notebook Jupyter ou Google Colab. O programa solicitará um tópico, e então os agentes trabalharão para encontrar, resumir e narrar uma história relacionada. A narração em áudio será reproduzida sequencialmente para cada parte da história.
