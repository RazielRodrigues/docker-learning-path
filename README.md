# DOCKER LEARNING PATH

    - NÃO É UM SISTEMA DE VIRTUALIZAÇÃO DE S.O
    - É UM SISTEMA DE ADMINISTRAÇÃO DE CONTÊINERES QUE SEPARA UM PROCESSO DE UM AMBIENTE
    - HOST E CONTAINER COMPARTILHAM O MEMSO KERNEL
    - EMPACOTA SOFTWARE COM VARIOS NIVEIS DE ISOLAMENTO
    - O CONTAINER TEM AS MESMAS CARACTERISTICAS DE UMA VM, PORÉM, COM MENOS CONSUMO DE MEMÓRIA
    - XLC X DOCKER
        - O DOCKER ABSTRAIU ESSA IDEIA, FAZENDO COM QUE O CONTAINER 
          SEJA UM PROCESSO MAIS FACIL DE SER MANIPULADO

#### CONTAINERS

    - SEGREGAÇÃO DE PROCESSOS NO MESMO KERNEL (ISOLAMENTO)
    - SISTEMAS DE ARQUIVOS CRIADOS A PARTIR DE UMA IMAGEM
    - AMBIENTES LEVE E PORTÁTEIS NO QUAL APLICAÇÕES SÃO EXECUTADAS
    - ENCAPSULA TODOS OS BINÁRIOS E BIBLIOTECAS NECESSÁRIAS PARA EXECUTAR UM PROGRAMA
    - UM CONTAINER DEVE SER MINIMALISTA, POR ISSO, NÃO DEVE TER MAIS DE UM PROCESSO
    - ALGO ENTRE UM CHROOT E UMA VM
        - CHROOT: APRISIONA ARQUIVO EM UMA PASTA
        - VM: AMBIENTE DE EXECUÇÃO COMPLETO
        - DOCKER: ISOLA O PROCESSO EM UM AMBIENTE SEPARADO

#### IMAGENS

    - MODELO DE SISTEMA DE ARQUIVOS SOMENTE-LEITURA USADO PARA CRIAR UM CONTAINER
    - IMAGENS SAO CRIADAS A PARTIR DE UM PROCESSO CHAMADO BUILD
    - SÃO ARMAZENADAS EM REPOSITORIOS NO REGISTRY (DOCKER HUB)
    - SÃO COMPOSTAS POR UMA OU MAIS CAMADAS (LAYERS)
    - UMA CAMADA REPRESENTA UMA OU MAIS MUDANÇAS NO SISTEMA DE ARQUIVO (COMO SE FOSSE UM COMMIT)
    - UMA CAMADA É TAMBÉM CHAMADA DE IMAGEM INTERMÉDIARIA POIS ELA 
      POSSUI OUTROS BINARIOS PARA O BINARIO QUE VOCE QUER FUNCIONAR
      E A JUNÇÃO DESSAS CAMADAS FORMAM AS IMAGENS
    - A APENAS A ULTIMA CAMADA PODE SER ALTERADA QUANDO O CONTAINER FOR INICIADO
    - AUFS (ADVANCED MULTI LAYERED UNIFICATION FILESSYSTEM) É MUITO USADO
    - O GRANDE OBJETIVO DESSA ESTRATEGIA DE DIVIDIR UMA IMAGEM EM CAMADAS É O REUSO
    - É POSSIVEL COMPOR IMAGENS A PARTIR DE COMANDOS DE OUTRAS IMAGENS
        - DOCKER.HUB

#### IMAGENS VS CONTAINERS

    - DOCKER HUB É COMO O GITHUB
    - IMAGENS SÃO CLASSES
    - CONTAINER SÃO OBJETOS
    - KITEMATIC

    - ARQUITEURA
        - DAEMON VAI NO REGISTRY E FAZ O DOWNLOAD DA IMAGEM
        - APOS ISSO FAZ UM CACHE DAS IMAGENS
        - CASO VOCE TENHA AS IMAGENS NA MAQUINA ELE  VAI USAR AS QUE JA TEM
            
#### INSTALAÇÃO

    - LINUX
        - DOCKER HOST É O PRIOPRIO LINUX
        - DOCKER DAEMON É O LINUX QUE VAI SER O HOST
        - DOCKER CLIENT É O LINUX QUE VAI SER O CLIENTE

    - MAC OS
        - O DOCKER HOST É UMA VM LINUX

    - WINDOWS
        - O DOCKER HOST É UMA VM LINUX NO WINDOWS
        - QUANDO TEM WSL É COMO SE EXECUTASSE NO LINUX


    - APOS O PRIMEIRO RUN A IMAGEM ESTA EM CACHE

#### CONTAINERS

    - O COMANDO RUN EXECUTA QUATRO COMANDOS
        - DOCKER IMAGEM PULL
        - DOCKER CONTAINER CREATE
        - DOCKER CONTAINER START
        - DOCKER CONTAINER EXEC

    - MODO DAEMON DEIXA RODANDO EM BACKGROUND
    - MODO ITERATIVO MODO DE TESTE
    - ARQUIVOS NÃO COMPARTILHADOS ENTRE CONTAINERS
    - O RUN SEMPRE CRIA UM NOVO CONTAINER
    - CONTAINERS DEVEM TER NOMES UNICOS

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