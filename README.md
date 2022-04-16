
<img src="...">

curso: https://www.udemy.com/course/curso-docker

# DOCKER
    - não é um sistema de virtualização de s.o
    - é um sistema de administração de contêineres que separa um processo de um ambiente
    - host e container compartilham o memso kernel
    - empacota software com varios niveis de isolamento
    - o container tem as mesmas caracteristicas de uma vm, porém, com menos consumo de memória
    - xlc x docker
        - o docker abstraiu essa ideia, fazendo com que o container 
          seja um processo mais facil de ser manipulado

#### CONTAINERS

    - segregação de processos no mesmo kernel (isolamento)
    - sistemas de arquivos criados a partir de uma imagem
    - ambientes leve e portáteis no qual aplicações são executadas
    - encapsula todos os binários e bibliotecas necessárias para executar um programa
    - um container deve ser minimalista, por isso, não deve ter mais de um processo
    - algo entre um chroot e uma vm
        - chroot: aprisiona arquivo em uma pasta
        - vm: ambiente de execução completo
        - docker: isola o processo em um ambiente separado

#### IMAGENS

    - modelo de sistema de arquivos somente-leitura usado para criar um container
    - imagens sao criadas a partir de um processo chamado build
    - são armazenadas em repositorios no registry (docker hub)
    - são compostas por uma ou mais camadas (layers)
    - uma camada representa uma ou mais mudanças no sistema de arquivo (como se fosse um commit)
    - uma camada é também chamada de imagem intermédiaria pois ela 
      possui outros binarios para o binario que voce quer funcionar
      e a junção dessas camadas formam as imagens
    - a apenas a ultima camada pode ser alterada quando o container for iniciado
    - aufs (advanced multi layered unification filessystem) é muito usado
    - o grande objetivo dessa estrategia de dividir uma imagem em camadas é o reuso
    - é possivel compor imagens a partir de comandos de outras imagens
        - docker.hub

#### IMAGENS VS CONTAINERS

    - docker hub é como o github
    - imagens são classes
    - container são objetos
    - kitematic

    - arquiteura
        - daemon vai no registry e faz o download da imagem
        - apos isso faz um cache das imagens
        - caso voce tenha as imagens na maquina ele  vai usar as que ja tem
            
#### INSTALAÇÃO

    - linux
        - docker host é o prioprio linux
        - docker daemon é o linux que vai ser o host
        - docker client é o linux que vai ser o cliente

    - mac os
        - o docker host é uma vm linux

    - windows
        - o docker host é uma vm linux no windows
        - quando tem wsl é como se executasse no linux


    - apos o primeiro run a imagem esta em cache

#### CONTAINERS

    - o comando run executa quatro comandos
        - docker imagem pull
        - docker container create
        - docker container start
        - docker container exec

    - modo daemon deixa rodando em background
    - modo iterativo modo de teste
    - arquivos não compartilhados entre containers
    - o run sempre cria um novo container
    - containers devem ter nomes unicos

#### CLI

    - docker container run hello-world (container de teste)
    - docker container run debian bash --version  (ver a versão do bash)

    - docker container ps (lista os containers ativos)
    - docker container ps -a (log dos comandos de containers)

    - docker container run --rm debian bash --version (executa e ja remove)
    - docker container run -it debian bash (entra no bash em modo iterativo)
    - docker container run -it --name container-teste debian bash (modo iterativo + nome customizado)

    - docker container ls (lista os containers)
    - docker container ls -a (lista os containers com logs)
    - docker volume ls (lista os volumes)

    - docker container run -p 8080:80 nginx (porta 80 do container para a porta 8080 do host)
    - docker container run -p 8080:80 -v c:/not-found:/usr/share/nginx/html nginx
    - docker container run -p 8080:80 -v <caminho arquivo>:/usr/share/nginx/html nginx
        -p
            onde 8080 é a porta que o meu pc acessa
            onde 80 é a porta que o container expoe o serviço nginx
        -v
            c:/not-found pasta que eu quero que o nginx veja na minha maquina
            /usr/share/nginx/html pasta do nginx para servir o conteudo
    - docker container run -d --name ex-daemon-basic -p 8080:80 -v <caminho arquivo>:/usr/share/nginx/html nginx
        - iniciando o container em modo de background
    
    - docker container start ex-daemon-basic (inicia o container)
    - docker container start -ai ex-daemon-basic (inicia o container em modo iterativo)
    - docker container restart ex-daemon-basic (reinicia o container)
    - docker container stop ex-daemon-basic (para o container)

    - docker container logs ex-daemon-basic (logs do container)
    - docker container inspect ex-daemon-basic (informações do container)
    - docker container exec ex-daemon-basic uname -or (Informações da versão do volume que roda)