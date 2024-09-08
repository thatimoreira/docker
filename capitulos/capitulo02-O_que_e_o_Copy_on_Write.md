# Capítulo II: O que é Copy on Write?

<br>

<h3 id="definicao">Definição</h3>

As **imagens** no Docker são compostas por várias camadas empilhadas. Cada vez que você executa um comando, como instalar um software ou alterar uma configuração, é criada uma nova camada.
Todas as camadas abaixo da última são **somente leitura (read-only)**, enquanto a última camada é **leitura e escrita (read-write)**. Isso significa que, quando um container está em execução, apenas a última camada pode ser modificada.<br><br>
___

<br>

<h3 id="o-que-e-copy-on-write?">O que é Copy on Write?</h3>

O conceito de **Copy on Write (COW)** define como as alterações são feitas em um container. Se você precisa modificar um arquivo que está em uma camada de leitura apenas, o Docker faz uma cópia desse arquivo na última camada
(a camada de escrita). Só depois dessa cópia você pode realizar modificações.

> **Exemplo**: Imagine que você quer fazer uma anotação em um livro. Em vez de escrever diretamente na página, uma cópia da página é criada, e é nessa cópia que você faz a anotação.<br><br>
> O **Docker** funciona da mesma forma: ele copia o arquivo de uma camada somente leitura para a camada de escrita antes de permitir a alteração.<br><br>

___

<br>

### Vantagens do Copy on Write

O **Copy on Write** permite que várias instâncias de containers usem a mesma imagem, economizando espaço em disco. Como as camadas inferiores são **somente leitura** e compartilhadas entre os containers,
não é necessário duplicar a imagem para cada container.

> **Exemplo comparativo com VMs**:  
> Se você tiver 10 containers usando uma imagem de 500 MB, o Docker utiliza apenas **500 MB** no total, pois a imagem é compartilhada entre todos os containers.<br><br>
> Por outro lado, se você tiver 10 **máquinas virtuais (VMs)** com uma imagem de 5 GB cada, o total será **50 GB**, pois cada VM precisa de uma cópia completa da imagem.  
> Isso mostra como o Docker é mais eficiente em termos de espaço.<br><br>
___

<br>

<h3 id="praticas-com-dockerfile">Práticas com Dockerfile</h3>

Quando criamos uma imagem no Docker usando um **Dockerfile**, cada instrução `RUN` adiciona uma nova camada.
Isso pode ser um problema quando fazemos operações como baixar e instalar pacotes, porque arquivos temporários que deveriam ser removidos podem acabar ocupando espaço desnecessário em camadas anteriores.<br><br>


#### Evitando camadas desnecessárias

Imagine que você adiciona as seguintes instruções ao Dockerfile:

```Dockerfile
RUN apt-get update
RUN apt-get install -y vim apache2
RUN apt-get clean
```

Nesse caso, cada comando RUN cria uma camada separada. O problema é que, quando você executa o apt-get clean em uma camada diferente da instalação dos pacotes, o Docker não consegue remover os arquivos temporários
criados durante o apt-get install das camadas anteriores. Isso acontece porque, no Docker, cada camada é read-only, ou seja, a limpeza dos arquivos não afeta as camadas anteriores, resultando em espaço desperdiçado.<br><br>


#### A solução: combinar comandos em uma única instrução RUN

Para evitar isso, o ideal é combinar múltiplos comandos RUN em uma única instrução, usando operadores como &&. Assim, você executa todas as operações necessárias dentro da mesma camada:

```Dockerfile

RUN apt-get update && apt-get install -y vim apache2 && apt-get clean
```

Dessa forma, o apt-get clean remove os arquivos temporários na mesma camada em que os pacotes foram instalados, otimizando o tamanho da imagem.

> Dica: Sempre que possível, combine instruções no Dockerfile para garantir que não haja resíduos de camadas anteriores, já que camadas read-only anteriores não podem ser alteradas.<br>

<br>

#### Por que evitar muitas camadas?

Cada camada em uma imagem Docker aumenta o tamanho total da imagem. Se você criar muitas camadas desnecessárias, o Docker armazena todas as versões intermediárias, mesmo que você não precise mais delas. Isso faz com que a imagem final ocupe muito mais espaço no disco do que o necessário.

Portanto, combine as instruções para evitar o acúmulo de camadas supérfluas e garantir que apenas as mudanças essenciais sejam preservadas.
