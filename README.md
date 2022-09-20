# Documentação da API do VMPay

### Descrição

Este é o projeto de documentação da API do VMPay.

Escrita em formato [reStructuredText](http://docutils.sourceforge.net/rst.html),
gerada usando o [Sphinx](http://sphinx-doc.org/),
hospedada no [Read The Docs](https://readthedocs.org/).

### Instalando o Sphinx

Há uma [documentação online](http://www.sphinx-doc.org/en/stable/install.html) de como instalar o Sphinx. Na [documentação completa do Read The Docs](http://docs.readthedocs.org/en/latest/) também há muita coisa.

Se você está no Linux Debian/Ubuntu pode instalar os pacotes necessários com os seguintes comandos:

```
sudo apt update

sudo apt install python3-sphinx

sudo apt install python3-pip

sudo apt install python3-stemmer

sudo -H pip install sphinx_rtd_theme
```


### Integrando este projeto com o Read The Docs

Há um [guia online](https://read-the-docs.readthedocs.org/en/latest/webhooks.html) de como integrar um projeto documentado com o Sphinx e hospedado no GitHub com o Read the Docs.

A integração deste projeto com o Read The Docs já foi feita. Ou seja, ao se dar um push para este repositório, a [documentação online](https://vmpay-api.readthedocs.io/en/latest/) hospedada no Read the Docs é atualizada automaticamente.

### Alterando a documentação

A documentação é gerada em HTML a partir dos arquivos .rst (reStructuredText):

1. Editar os arquivos .rst desejados. O [guia rápido do reStructuredText](http://sphinx-doc.org/rest.html) tem todo o básico que se precisa saber;

2. Gerar a documentação em HTML:

   ```cd docs; make html```

3. A documentação em HTML será gerada dentro do diretório `build/html`. Este diretório não é commitado, serve somente para verificação local;

4. Abrir o arquivo `build/html/index.html` no browser de sua preferência. Se estiver tudo ok, commitar e dar push para este repositório. A documentação será automaticamente gerada e disponibilizada no Read The Docs.

### Onde ler a documentação da API do VMPay

A documentação em formato legível está [aqui](https://vmpay-api.readthedocs.io/en/latest/).
