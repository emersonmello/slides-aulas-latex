# Como organizar slides de aulas com LaTeX e git

- Crie um subdiretório específico para cada aula. Esse diretório só terá o arquivo `.tex` e as figuras específicas para a aula em questão.
  - Quando fizer uma nova aula, use modelo o arquivo `.tex` de uma das aulas anteriores.
- O diretório [`0-ifscyan-modelo`](0-ifscyan-modelo) contém o arquivo `.sty` do modelo LaTeX Beamer, além da figura com o logo da instituição. Dessa forma, esses arquivos não serão replicados em cada uma das aulas.

Abaixo é apresentada a estrutura proposta. No exemplo, tem-se duas aulas, cada qual em seu próprio diretório.

```
.
├── 0-ifscyan-modelo
│   ├── beamerthemeifscyan.sty
│   └── figs
│       └── ifsclogo.pdf
├── aula01
│   ├── aula01.tex
│   └── figs
│       └── git-branch.png
└── aula02
    └── aula02.tex
```

## Fluxo de trabalho com o git

- Não misture, em um mesmo *commit*, alterações em diferentes aulas
- No final do semestre marque com uma *tag* o último *commit*. Por exemplo, `git tag 2019-02`. Isso permitirá recuperar o conjunto de aulas por semestre


## Captura de telas 

Abaixo um exemplo de slides gerado com o modelo presente nesse repositório.

![demo](demo.png)

### Proporção 16x9 (widescreen)

![Prova](screenshots/wide.png)
### Outras cores

![amarelo](screenshots/amarelo.png)
![azul](screenshots/azul.png)
![bordo](screenshots/bordo.png)
![cinza](screenshots/cinza.png)
![marrom](screenshots/marrom.png)
![roxo](screenshots/roxo.png)

## Configurações do Visual Studio Code

O Visual Studio Code possui a extensão [LaTeX Workshop](https://marketplace.visualstudio.com/items?itemName=James-Yu.latex-workshop) que o torna uma IDE LaTeX. Abaixo deixo algumas configurações pessoais que criei para facilitar a edição de slides LaTeX/Beamer com o Visual Studio Code.

Da forma que fiz, ao salvar um documento, o VSCode irá automaticamente compilar e gerar o PDF. A visualização do PDF ficará no painel lateral (precisará clicar no ícone na parte superior da direita).

### User Snippets

- Abra o Visual Studio Code, vá em *Preferences* -> *User snippets* e edite o arquivo `latex.json`. Coloque o seguinte conteúdo dentro:

```json
{
"Beamer frame":{
		"prefix": "frame",
		"body": ["\\begin{frame}{$1}\n\\begin{itemize}\n\t\\item $0\n\\end{itemize}\n\\end{frame}"],
		"description": "LaTeX Beamer frame env"
	},
	"LaTeX itemize env":{
		"prefix": "itemize",
		"body": ["\\begin{itemize}\n\t\\item $0\n\\end{itemize}"],
		"description": "itemize env"
	},
	"Beamer block":{
		"prefix": "block",
		"body": ["\\begin{block}{$1}\n\t $0\n\\end{block}"],
		"description": "LaTeX Beamer block"
	},
	"LaTeX column env":{
		"prefix": "columns",
		"body": ["\\begin{columns}\n\t\\column{.5\\linewidth}\n\t $0\n\t\\column{.5\\linewidth}\n\t \n\\end{columns} "],
		"description": "columns env"
    },
    "LaTeX figure env":{
		"prefix": "figure",
		"body": ["\\begin{figure}[ht]\n\t\\centering\n\t\\caption{$2}\n\t\\label{fig:$0}\n\t\\includegraphics[width=\\linewidth]{$1}\n\\end{figure}"],
		"description": "LaTeX figure env"
    },
    "LaTeX includegraphics beamer":{
		"prefix": "includegraphics",
		"body": ["\\begin{center}\n\t\\includegraphics[width=\\linewidth]{figs/$0}\n\\end{center}"],
		"description": "LaTeX includegraphics"
    },
    "LaTeX beamer only":{
		"prefix": "only",
		"body": ["\\only<${1|1,2,3,4,5,6|}>{\n\t$0\n}"],
		"description": "LaTeX beamer only"
    },
    "Beamer only env":{
		"prefix": "onlyenv",
		"body": ["\\begin{onlyenv}<${1|1,2,3,4,5,6|}>\n\t $0\n\\end{onlyenv}"],
		"description": "LaTeX Beamer Only env"
    },
    "Lstlisting":{
		"prefix": "lstlisting",
		"body": ["\\begin{lstlisting}[style=$1]\n$0\n\\end{lstlisting}"],
		"description": "Lstlisting env"
    }
}
```

Esses `snippets` são atalhos para gerar comandos em LaTeX. Por exemplo, sempre que eu preciso criar um novo slide eu só digito `frame` e no popup que aparece eu escolho o `frame` e pressiono ENTER. Dessa forma o Visual Studio Code gera o seguinte bloco:

```latex
\begin{frame}{}
\begin{itemize}
    \item 
\end{itemize}
\end{frame}
```

### Settings

- Abra o Visual Studio Code, vá em *Preferences* -> *Settings*. Mude para o modo que visualiza o conteúdo do arquivo `settings.json` (basta clicar em ícone que fica na parte superior do lado direito).  

- Adicione o seguinte trecho dentro do bloco já existente (o bloco é delimitado por { e })

```json
"latex-workshop.bibtex-fields.sort.enabled": true,
"latex-workshop.bibtex-format.sort.enabled": true,
"latex-workshop.latex.clean.subfolder.enabled": true,
"latex-workshop.latex.outDir": "%DIR%/outlatexdir",
"latex-workshop.view.pdf.viewer": "tab",
"latex-workshop.view.pdf.zoom": "page-width",
"latex-workshop.synctex.afterBuild.enabled": true,
"git.autoStash": true,
"editor.bracketPairColorization.enabled": true,
"files.exclude": {
    "**/.classpath": true,
    "**/.project": true,
    "**/.settings": true,
    "**/.factorypath": true,
    "**/*.class": true,
    "**/*.bbl": true,
    "**/*.bcf": true,
    "**/*.nav": true,
    "**/*.snm": true,
    "**/*.aux": true,
    "**/*.fls": true,
    "**/*.blg": true,
    "**/*.idx": true,
    "**/*.ind": true,
    "**/*.lof": true,
    "**/*.lot": true,
    "**/*.lol": true,
    "**/*.out": true,
    "**/*.acn": true,
    "**/*.acr": true,
    "**/*.alg": true,
    "**/*.glg": true,
    "**/*.glo": true,
    "**/*.gls*": true,
    "**/*.ist": true,
    "**/*.log": true,
    "**/*.fdb_latexmk": true,
    "**/*.synctex*": true,
    "**/*.run.xml": true,
    "**/*.toc": true,
    "**/*.vrb": true
  }
  ```

  Isso fará com que todos os arquivos auxiliares da compilação do `.tex` sejam colocados dentro de um subdiretório `outlatexdir`. O PDF resultando também será colocado dentro desse subdiretório.

  Isto também fará que arquivos auxiliares não sejam listados no painel explorador de arquivos do Visual Studio Code.

### Teclas de atalho

Abaixo criei teclas de atalho para os comandos que deixam o texto em **negrito**, *itálico* e typewriter.

```json
// Place your key bindings in this file to overwrite the defaults
[
{
    "key": "crtl+b",
    "command": "editor.action.insertSnippet",
    "when": "editorTextFocus && editorLangId == latex",
    "args": {
        "snippet": "\\textbf{${TM_SELECTED_TEXT}}$0"
    }
},
{
    "key": "crtl+i",
    "command": "editor.action.insertSnippet",
    "when": "editorTextFocus && editorLangId == latex",  // chained clause
    "args": {
        "snippet": "\\textit{${TM_SELECTED_TEXT}}$0"
    }
},
{
    "key": "crtl+t",
    "command": "editor.action.insertSnippet",
    "when": "editorTextFocus && editorLangId == latex",  // chained clause
    "args": {
        "snippet": "\\texttt{${TM_SELECTED_TEXT}}$0"
    }
}
]
```