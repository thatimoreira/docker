# Capítulo I: O que é um Container?

<br>

<h3 id="definicao">Definição</h3>

Um **container** é como uma caixinha que guarda tudo o que um programa precisa para rodar. Dentro dessa caixinha, você tem o código do programa, as dependências (como bibliotecas e ferramentas) e as configurações. Isso significa que, não importa onde essa caixinha seja levada (no seu computador, em um servidor, ou na nuvem), o programa sempre vai funcionar da mesma forma.

Containers têm uma função muito importante: eles **isolam os recursos lógicos e físicos** do sistema. Isso quer dizer que o programa dentro do container usa seus próprios arquivos, variáveis e bibliotecas, sem interferir no que está fora. Ao memso tempo, ele também usa apenas os **recursos computacionais** (como memória e CPU) que realmente precisa, o que permite **aproveitar ao máximo o desempenho** do sistema sem desperdiçar capacidade.<br><br>
___

<br>

### Tipos de Isolamento

#### 1. Isolamento Lógico
O **isolamento lógico** garante que os processos, usuários e redes de cada container sejam independentes dos outros. Isso significa que, dentro de um container, você só verá os processos que pertencem a ele, mesmo que, no sistema host (servidor), todos os processos estejam visíveis.

- **Processos isolados**: Dentro de um container, apenas os processos que pertencem a ele são visíveis. Se você rodar um comando como `ps` dentro do container, verá apenas os processos específicos dele. Os processos de outros containers ou do próprio sistema host não aparecem. Isso cria uma camada de segurança e separação entre os containers.
  
- **Usuários isolados**: Cada container também pode ter seu próprio sistema de usuários. Isso significa que os usuários definidos dentro de um container são independentes dos usuários de outros containers ou do sistema principal.
  
- **Rede isolada**: Cada container tem sua própria configuração de rede. Isso significa que os containers podem ter seus próprios endereços IP, roteamentos e portas, sem conflito com outros containers. Mesmo que vários containers estejam rodando no mesmo servidor, suas conexões de rede não interferem entre si.

- **Montagem dos mountpoints** (pontos de montagem): Dentro de um container, você pode ter diferentes volumes ou diretórios montados, e eles são isolados dos mountpoints de outros containers. Isso garante que os arquivos e sistemas de arquivos usados em um container não estejam acessíveis aos outros containers.
   > **Nota:** Um **mountpoint** é um local onde sistemas de arquivos adicionais (como discos ou volumes) podem ser conectados e acessados. Quando você monta um sistema de arquivos em um mountpoint, ele passa a ser tratado como parte do diretório do sistema principal.<br><br>
   > No contexto de containers, mountpoints são usados para conectar volumes externos ou compartilhados, permitindo que os containers acessem ou armazenem dados fora do seu ambiente isolado.

<br>

#### 2. Isolamento Físico
Além do isolamento lógico, os containers também permitem isolar **recursos físicos**, como CPU, memória e taxa de I/O (entrada/saída), para que cada container use apenas o que foi dedicado a ele.

- **CPU e Memória**: Você pode limitar a quantidade de CPU e memória que um container pode usar. Por exemplo, você pode configurar um container para usar apenas um núcleo de CPU ou 512 MB de RAM, garantindo que ele não consuma mais do que isso.

- **Taxa de I/O**: Também é possível controlar a quantidade de leitura e escrita que o container pode fazer no disco (I/O de disco) ou na rede. Isso impede que um container consuma todos os recursos do sistema, o que poderia afetar o desempenho de outros containers.<br><br>
___

<br>

### Mecanismos de Isolamento

O isolamento de containers é possível graças a dois mecanismos importantes presentes no kernel do Linux: **namespaces** e **cgroups**.

- **Namespaces**: São responsáveis pelo isolamento lógico. Eles criam ambientes separados dentro do sistema, garantindo que cada container tenha sua própria visão dos recursos, como processos, rede e usuários. Isso faz com que os containers funcionem como se fossem sistemas independentes, mesmo estando no mesmo servidor físico. Cada container tem seus próprios **namespaces**, isolando seus recursos dos demais.

- **Cgroups (Control Groups)**: São responsáveis pelo isolamento físico. Os **cgroups** permitem limitar e monitorar o uso de recursos do sistema, como CPU, memória e I/O, para cada container. Isso garante que um container não consuma mais recursos do que foi definido, permitindo um controle preciso sobre o uso dos recursos físicos no sistema.<br><br>
___

<br>

### Importância dos Containers

Os containers são muito importantes porque eles tornam o desenvolvimento e a execução de programas mais fáceis e eficientes. Eles permitem **aproveitar ao máximo os recursos do sistema** sem a necessidade de criar camadas pesadas de abstração, como acontece com máquinas virtuais. Em vez de rodar um sistema operacional completo para cada aplicação, como acontece com VMs (máquinas virtuais), o container apenas isola os recursos necessários para aquela aplicação específica.

Isso faz dos containers uma solução extremamente leve e eficaz para rodar várias aplicações no mesmo servidor, com controle sobre o que cada uma pode acessar e usar, garantindo **eficiência, isolamento e segurança**.
