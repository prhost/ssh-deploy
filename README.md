# Docker image para copiar arquivos (rsync) e executar comandos remotamente (SSH)

## Exemplo de uso no Gitlab CI

```
Upload files:
  image: "prhost/ssh-deploy"
  variables:
    HOST: "servidor.com.br" # host ou ip do servidor
    IP: "111.111.111.111" # ip do servidor
    SSHKEY_PRIVATE: $SSH_PRIVATE_KEY # texto da chave privada. Recomendado usar variables do Gitlab
    USER_HOST: "root" # usuario do ssh
    PUBLIC_DIRECTORY: "/var/www/html" # pasta inicial onde o ssh vai se conectar
    SOURCE_DIR: $CI_PROJECT_DIR # pasta do projeto no gitlab
    IGNORE_FILES: ".env.example .git/ .gitignore" # Define quais arquivos gostaria de ignorar no upload
    DELETE: "true" # Se true, vai sobrescrever os arquivos e pastas existentes, se false vai mesclar com os arquivos e pastas
    FILES: "index.php .htaccess app/ vendor/" # Arquivos e pastas que devem ser copiadas
  script:
    - ssh-deploy

Execute remote command:
  image: prhost/ssh-deploy
  variables:
    HOST: "servidor.com.br" # host ou ip do servidor
    IP: "111.111.111.111" # ip do servidor
    SSHKEY_PRIVATE: $SSH_PRIVATE_KEY # texto da chave privada. Recomendado usar variables do Gitlab
    USER_HOST: "root" # usuario do ssh
    SOURCE_DIR: $CI_PROJECT_DIR # pasta do projeto no gitlab
    EXEC_SCRIPT: "ls -la"
  script:
    - ssh-exec
```

### Pacotes usados

* https://github.com/Gruppio/Echolor
