# Install and configure 

## Install prerequirment software


```sh
add-apt-repository ppa:git-core/ppa
sudo apt-get update
sudo apt-get install     ca-certificates     curl     gnupg     lsb-release
sudo apt-get install docker-ce docker-ce-cli containerd.io
sudo apt-get install docker-ce docker-ce-cli containerd.io
sudo apt install apt-transport-https ca-certificates curl software-properties-common

sudo apt-get update
sudo apt-get update && sudo apt-get upgrade
sudo apt-get install docker-ce docker-ce-cli containerd.io
sudo apt-get install pyhton3
sudo apt install python3-pip
```

## Install mkdocs
```sh
sudo apt install mkdocs

mkdocs new .
pip install -e mkdocs-material
git submodule add https://github.com/squidfunk/mkdocs-material.git mkdocs-material

# run in docker
sudo docker run --rm -it -p 8000:8000 -v ${PWD}:/docs squidfunk/mkdocs-material

mkdocs build
mkdocs serve
mkdocs serve --livereload

mkdocs gh-deploy --force
```

## Plugin install
```sh
pip install git+https://github.com/jldiaz/mkdocs-plugin-tags.git
pip install mkdocs-minify-plugin>=0.3.0
pip install mkdocs-awesome-pages-plugin>=2.5.0
pip install mkdocs-macros-plugin>=0.5.0
pip install mkdocs-redirects>=1.0.1
pip install mkdocs-git-revision-date-plugin>=0.3.1
pip install testresources
pip install mkdocs-git-revision-date-plugin>=0.3.1
pip install mkdocs-git-revision-date-localized-plugin>=0.8
pip install tags
pip install mkdocs-git-revision-date-plugin && pip install mkdocs-minify-plugin
```

## Usefull link

(1) [Official page](https://www.markdownguide.org/getting-started/)<br/>
(2) [Basic syntax](https://www.markdownguide.org/basic-syntax/)<br/>
(3) [Github page](https://docs.github.com/en/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax)<br/>
(4) [Mardown reference](https://docs.microsoft.com/pl-pl/contribute/markdown-reference) **PL**<br/>
(5) [MkDocs](https://www.mkdocs.org/)<br/>
(6) [MkDocs Github](https://squidfunk.github.io/mkdocs-material/getting-started/)<br/>
(7) [Mkdocs navigation](https://squidfunk.github.io/mkdocs-material/setup/setting-up-navigation/#navigation-sections)

## Usefull Bootstrap icons

[Empty star](https://www.codesprogram.com/icons/Star-o-icon-in-font-awesome) <i class="fa fa-star-o" style="font-size:12px"></i><br/>
[Half star](https://www.codesprogram.com/icons/Star-half-o-icon-in-font-awesome) <i class="fa fa-star-half-o" style="font-size:12px"></i> <i class="fa fa-star-half-o fa-spin" style="font-size:12px"></i><br/>
[Full star](https://www.codesprogram.com/icons/Star-icon-in-font-awesome) <i class="fa fa-star" style="font-size:12px"></i><br/>




