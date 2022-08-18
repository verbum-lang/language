### <b>Packaging</b>

****

Em linhas gerais, o <b>gerenciador de pacotes da linguagem</b> deve ser o máximo <b>livre</b> possível, e <b>totalmente descentralizado</b>. 

Para realizar esta descentralização dos pacotes da linguagem, isto é, podendo assim qualquer pessoa escrever um novo módulo, a suite da linguagem possui um gerenciador que inicialmente verifica num <b>mirror</b> padrão a existência dos pacotes, este mirror, trata-se do repositório existente no repositório oficial do projeto da linguagem no Github (package manager). E o mesmo possui como finalidade apenas armazenar os links dos repositórios dos módulos, que podem estar armazenados em qualquer outro repositório git.

Logo, o gerenciador de pacotes apenas seleciona o link git, para então realizar uma cópia do respectivo módulo/pacote, e instalá-lo para uso em projetos.

Esta instalação deve ser tanto local, como definitiva, no repositório de instalação padrão da linguagem.

Desta maneira é possível baixar utilizando a lista de repositórios oficiais, bem como instalar diretamente de algum link git.

Utilizando a mesma noção, uma vez que um projeto utilize de um pacote em específico, o mesmo é informado num arquivo <b>JSON de configurações</b>, semelhante ao <b>package.json</b> de projetos Node JS. Com uma seção especial para as <b>dependências</b>.

De modo que ao baixar um projeto, e nele conter as N-dependências, todas elas vem junto consigo os links de seus respectivos diretórios git, e desta maneira são todos instalados, nas versões mais recentes, diretamente dos repositórios oficiais.

<b>Futuramente será definida uma política de organização dos pacotes.</b>


