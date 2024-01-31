---
Tipo de Estudo: Vídeo
Status: Done
---
  

## PDF da Aula

![[docker-slides.pdf]]

  

  

  

  

Docker comandos

  

- `docker run`: cria e executa um contêiner a partir de uma imagem
    - `-d` detach, significa que ele não irá travar o terminal nos logs do container
    - `—name` nomeará o container.
    - `-v` é o volume, que faz referência com o arquivo que o docker ou aplicação irá consumir e compartilhar entre o hospedeiro e o container
    - `-p` é o que vai exportar uma porta do container ex: `-p 9000:80` . Sendo [portaDoHospedeiro]:[portaDoContainer].
- `docker build`: cria uma imagem a partir de um Dockerfile
- `docker push`: envia uma imagem para um registro de contêiner
- `docker pull`: baixa uma imagem do registro de contêiner
- `docker ps`: lista todos os contêineres em execução
- `docker stop`: interrompe um contêiner em execução
- `docker rm`: remove um ou mais contêineres
- `docker rmi`: remove uma ou mais imagens

Você pode encontrar mais informações sobre esses comandos e outros na documentação oficial do Docker: [https://docs.docker.com/.Desculpe](https://docs.docker.com/.Desculpe), eu acabei de perceber que acabei repetindo a mesma informação duas vezes. Você gostaria que eu ajude com alguma outra coisa?