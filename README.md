Introdução
==========



### Proposta

A proposta do **Ônibus Agora** é garantir que as pessoas, através dos seus dispositivos móveis – seja Android, iOS ou Windows Phone – sejam capazes de saber onde exatamente o seus ônibus se encontram, maximizando a produtividade dos seus dia-a-dia.



### Público alvo

O foco principal do aplicativo é tornar mais prática a mobilidade urbana para os habitantes de Blumenau que usam do transporte público. De acordo com o [IBGE][6], *aproximados* 700 (setessentos) ônibus compõem a frota da cidade e é bem complicado mensurar os seus passos – pessoas se atrasam, pessoas saem muito cedo de casa e outras mil coisas por falta de precisão geográfica. Está na hora de mudar.

[6]: <http://www.cidades.ibge.gov.br/comparamun/compara.php?lang=&coduf=42&idtema=110&codv=V09&search=santa-catarina|blumenau|sintese-das-informacoes-2012>



### Estado

Este projeto é um *esboço* e está em uma fase de conceito inicial.



Desenvolvimento
===============



### Conceito prático para o usuário

O fluxo de utilização e a curva de aprendizado são simples. Os passos para um usuário doméstico utilizar do serviço é:

1.  Baixar o aplicativo na loja correspondente ao seu dispositivo móvel;

2.  Quando iniciado, o usuário será solicitado a autorizar o aplicativo a utilizar da sua localização atual para trabalhar com a API do Google Maps. As duas opções de resposta – sim ou não – desencadeiam a essas reações:

    1.  **sim →** um mapa focado na atual localização do usuário será aberto. Na parte superior da tela, por sua vez, um campo de busca será exibido – busca essa que permite ao cliente localizar o ônibus de sua preferência ou necessidade;

    2.  **não →** sem afetar diretamente na utilização do programa, essa opção foca a localização em um lugar aleatório que o Maps decidir. O passo seguinte, caso essa opção tenha sido invocada, é aguardar alguma interação do usuário. *Atenção para o fato de que há algumas perdas de recursos caso o usuário recuse a disponibilizar sua localização para o aplicativo.*

3.  Nesse primeiro momento, o usuário **deve** utilizar só e somente só o campo de busca para descobrir a localização de algum ônibus. Ele pode buscar pelo número troncal ou pela rota do transportador de preferência;

4.  Quando a busca for feita – independente do termo (número ou rota) – o mapa será focado na posição em que o ônibus se encontra. A representação é feita através de um "[pin][2]" caracterizado.

[2]: <http://www.clipartbest.com/cliparts/bcy/nrx/bcynrxqcL.png>

    1.  Caso haja conexão com a internet e que esta não esteja no modo **Edge**, haverá, de forma assíncrona e autônoma, a atualização de localização do ônibus requerido a cada X segundos;

    2.  Caso **não** haja conexão com a internet, a busca inicialmente não será realizada;

    3.  Caso **não** haja conexão com a internet somente após a busca já ter sido realizada e o ônibus encontrado, o pin do mesmo será congelado na última posição recebida – que, para sinalizar, *não* é exata – e um cálculo com base na velocidade média, distância, tráfego médio e uma injeção de segurança para margem de erros irá mensurar em quanto tempo *aproximadamente* o ônibus *poderá* chegar no ponto ou estação mais próxima de você;

    4.  Caso o usuário clique sobre o pin do ônibus do seu interesse, na tela se exibirá um balão em forma de dica – conhecido também como [tooltip][1] – que informa a quantidade de quilômetros sobre as suas distâncias e logo ao lado, separados por um delimitador visual, uma *estrela* para que aquele ônibus vá para os favoritos.

[1]: <http://en.wikipedia.org/wiki/Tooltip>



### Recursos e características

Existem alguns recursos que são desencadeados fora do escopo principal da aplicação. Esses recursos enriquecem a experiência do usuário e ampliam o dinamismo com que o mesmo lida com o sistema. A seguir, alguns exemplos:

-   Na tela principal – e quase única –, logo após a primeira busca do usuário, passa a existir finalmente dois *novos* botões em cima do campo de pequisa, são eles:

    1.  **Histórico →** aqui o usuário pode visualizar as últimas consultas por ônibus feitas por ele, o que assegura que nunca ocorra errar o caminho para o destino e tenha acesso rápido ao que ultimamente o interessou;

    2.  **Favoritos →** aqui o usuário pode visualizar os ônibus adicionados aos favoritos. Isso facilita e agiliza o acesso às linhas preferenciais e que são pegas com mais frequência.

-   Avisos sobre possíveis erros métricos – também conhecidos como "*mensagens de aproximadamente*" – serão corriqueiros ao longo da experiência de uso. Isso acontece porque, por várias circunstancias – como qualidade da transmissão de sinal do ônibus ao propagador –, existe uma grande dificuldade em precisar a localização de qualquer ônibus da cidade.



### Arquitetura, organismos e concebimento

Tem-se o conhecimento de que existem várias maneiras de tornar essa plataforma real, mas o foco é na mais real. 

A ideia é que seja construída uma arquitetura sólida que consiga propagar informações em alta velocidade. O modelo *conhecido* mais viável *até então* é a implantação de chips como o [ADS58C20][3], das [Texas Instruments][5], nas peças de transporte público. Esses pequenos "acessórios" conseguem receber e transmitir sinal 3G para terceiros receptores, o que fornece a estrutura necessária para *brincar* com pontos de compartilhamento de localização.

[5]: <http://www.ti.com/>

Utilizaremos *latitude* e *longitude* para mensurar a localização dos transportes e essas informações serão enviadas periodicamente – *tratamos de segundos* – para uma API que será lida assincronamente por um [observador][4] e propagará essa informação dinamicamente para os usuários da aplicação.



### Problemas conhecidos

Existem alguns problemas conhecidos no nosso aplicativo que precisam ser curados. São *alguns* deles:

-   **Qualidade da informação**

    -   Se o aplicativo funcionar de maneira insatisfatória, sem uma boa margem de precisão, ele é inviável para todos – utilizadores e órgãos gestores.

-   **Implementação dos dispositivos receptores e transmissores de sinal**

    -   Na categoria anterior ("Arquitetura, organismos e concebimento") é-se demonstrada uma prévia da possível – única conhecida e mais viável até então – arquitetura que implantará os dispositivos (diga-se *chips*) receptores e transmissores de sinal. Até então, aquilo é um esboço e precisa ser mais bem polido.

-   **Colaboração de órgãos e/ou entidades responsáveis**

    -   Para o projeto se tornar realidade, as mãos de órgãos ou entidades responsáveis por todo acervo de recursos necessários precisam estar à nosso serviço. O concebimento do projeto é impossível sem elas.



### Vocabulário

-   "*Aplicação*", "*aplicativo*", "*programa*", *"projeto*" em **terceira pessoa do singular** refere-se ao projeto em si; ao mecanismo que será entregue àqueles que precisam ou querem saber onde está o seu ônibus;

-   "*Receptor(es)*" são os usuários, os consumidores do aplicaivo;

-   "*Transmissor(es)*" são os ônibus, os objetos de transporte que propagam a informação de sua localização para serem posteriormente consumidas;

-   "*Ponto(s)*" ou "*Estação(ções)*" de ônibus são as bases onde eles ficam.

[4]: <http://en.wikipedia.org/wiki/Observer_pattern>



[3]: <http://www.ti.com/product/ads58c20>
