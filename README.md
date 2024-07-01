# Tecnologia utilizadas
- Docker
- AWS
- Github Actions

# Instalação:

Pré Requisitos: 
- Docker

Inicialmente, clonar o repositorio em questão para dentro da máquina e iniciar o projeto em questão
```
git clone https://github.com/gabrielphi/docker-nginx-php-basic.git ; cd docker-nginx-php-basic 
```

Para iniciar o projeto

```
docker compose up -d
```

Para acessar, use o seu IP Publico ou localhost.

OBS: Aplicação usa porta 80, não pode haver conflitos na porta respectiva na hora de inicializar.

# Informações e detalhes dos projetos.

## dockerfile
- Dockerfile foi criado com o intuito de realizar uma build especifica do php-fpm, o container em si estava com um bug relacionado ao PDO na hora de conectar ao banco de dados, o mesmo não estava conectando, com isso foi criado uma build especifica do PHP e compilada no docker-compose para que corrija o erro e suba um container com as informações corrigidas.

## nginx e site.conf
- **site.conf**: Foram adicionadas as seguintes configurações ao arquivo base *LISTEN 80* , *allow all* para realizar a liberação das comunicações externas que poderiam vir, isso somando a configuração de fireawll padrão do AWS, tecnologia que foi utilizada para esse projeto. *root* definiu o diretório padrão do projeto, diretório esse que foi transferido os arquivos necessários ao container na inicialização do docker-compose. Dentro do site.conf ainda foi realizado a configuração do container do php.

- **nginx**: Foi colocado as informações dos volumes que são os arquivos necessários conforme citado acima, mas em especialmente o arquivo *site.conf* foi substituido pelo arquivo *default.conf* dentro do container, para garantir que a página web que ele pegue, seria esta. Não foram realizadas configurações de redirecionamento.

## index.php
- **index.php**: A página inicial do projeto existe a configuração gethostname() apenas para fins de testes relacionados ao LoadBalancer, e emite um texto escrito "Conectado com sucesso" quando a conexão com o banco de dados mysql é efetuada com sucesso. Não foi realizada a execução de um select, mas o mesmo poderia ser colocado logo abaixo da conexão, iniciando com um insert e seguido por um select.

  
