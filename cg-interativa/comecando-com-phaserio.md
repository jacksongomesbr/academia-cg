# Começando com phaser.io

[phaser.io](http://phaser.io/) é um framework HTML5 para desenvolvimento de jogos em plataforma desktop e mobile. Com a popularização do desenvolvimento front-end, baseado em HTML5, no aumento do desempenho e da popularidade dos browsers, tanto em desktop quanto mobile, a utilização de um framework dessa natureza é bastante razoável. Este capítulo apresenta um guia inícial para o desenvolvimento de jogos com phaser.io.

## Servidor Http

Software desenvolvido com phaser.io precisa ser fornecido para o usuário por meio do protocolo Http. Isso significa que abrir um arquivo html diretamente no browser \(o que irá usar o protocolo `file:///`\) não irá funcionar.

Para resolver essa questão é necessário utilizar um servidor Http para entregar os arquivos do software para o browser. Dentre as várias opções possíveis para isso, vamos utilizar o pacote `http-server` para o NodeJs. No prompt de comando, execute:

```
npm install --save-dev http-server
```

Isso fará com que o http-server esteja disponível no caminho `node\\`_`modules/.bin/http-server` ou `node`_`modules/.bin/hs`.



