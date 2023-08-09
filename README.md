# Manual do sistema PAI

## Pré-requisitos funcionais
1. Crie um repositório no github marcando a opção "público", adicionando README.md, arquivo .gitignore para Python e a licença GPL v3

2. Clone o repositório na máquina local e abra-o no Powershell
    
3. Prepare o ambiente no powershell com as instruções:
    ``` 
    $ python -m venv venv
	$ cd .\venv\Scripts\
	$ .\activate
	$ python.exe -m pip install --upgrade pip
	$ cd..
	$ cd..
	$ pip install mkdocs-material
	$ code . # para abrir no vscode
    ```

4. Dentro do vscode, abrir o terminal e rodar:
    ```
    $ mkdocs new
	$ mkdocs serve
    ```
    O ambiente estará operacional localmente.

5. Edite o site

6. Na raiz do projeto, crie os diretórios: /.github/workflows

7. Crie, na pasta workflows, um arquivo de automatização chamado ci.yml, nele entre com:
    ```
    name: ci 
    on:
    push:
        branches:
        - master 
        - main
    permissions:
    contents: write
    jobs:
    deploy:
        runs-on: ubuntu-latest
        steps:
        - uses: actions/checkout@v3
        - uses: actions/setup-python@v4
            with:
            python-version: 3.x
        - uses: actions/cache@v2
            with:
            key: ${{ github.ref }}
            path: .cache
        - run: pip install mkdocs-material
        - run: mkdocs gh-deploy --force
    ```

8. Finalize a automatização do deploy indo no github em Settings > Pages e marcando as opções de gh-pages e root como ponto de partida do deploy. 

Em alguns minutos o site estará hospedado! :-)
