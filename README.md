# Buildando o MOPAC

## Introdução

Neste tutorial, vamos aprender como baixar e construir o Mopac. Vamos incluir imagens para facilitar o entendimento.

## Pré-requisitos

- Sistema operacional compatível (Linux, macOS, Windows)
- Git instalado
- Compilador Fortran (gfortran, ifort)
- Biblioteca blas e lapack (Usuários do ubuntu - _sudo apt-get install libopenblas-dev_)

## Baixando o MOPAC

Primeiro, vamos clonar o repositório do MOPAC do GitHub.

Clique nesse [link](https://github.com/openmopac/mopac) para abrir a pagina inicial do github do MOPAC.

![mopac-github-1](https://drive.google.com/uc?export=view&id=1IqusZJGibJ8a10UqVZ2iMct69kx3vVTH)

Em seguida, vamos pegar o endereço do repositório para fazer o clone.

O endereço pode ser encontrado aqui:

![mopac-github-2](https://drive.google.com/uc?export=view&id=1--JISsNJT4ULhu2QkdpKX3diYX1m-83D)

    Obs.: Caso tenha uma chave SSH cadastrada no Github, é altamente recomendado usar o endereço SSH.

Com o endereço em mãos, vamos baixar ele usando o git. No terminal digite o seguinte comando:

```sh
git clone https://github.com/openmopac/mopac.git
```


## Buildando o projeto

A partir daqui é recomendando o uso de um editor de texto (VSCode, Sublime e etc) para uma melhor experiencia, em nossos exemplos utilizaremos o VSCode.

No diretório raiz do projeto (na raiz do projeto você encontra o arquivo CMakeLists.txt)

crie uma pasta chamada build

```sh
mkdir build
```
Abra a pasta build

```sh
cd build
```

Agora para segue o comando do cmake para criar os arquivos de build:

```sh
cmake ../
```

![cmake-command](https://drive.google.com/uc?export=view&id=1ZTFvDSGAXuRY6qX-2bRBpOGlzj6U3vUG)



Em seguida, execute o comando make, para fazer o build do projeto.

```sh
make
```
Temos uma forma de fazer o build em _paralelo_ adicionando ao comando _make_ uma flag adicional.

```sh
make -j numero_de_processos
```

O comando acima você controla quantos processos o make vai criar para estar buildando em paralelo o projeto.

Para utilizar todos os núcleos da maquina utiliza o comando:

```sh
make -j $(nproc)
```

### Comando adicionais de build

Para o CMake temos algumas configurações para o projeto

#### 1. Usando o compilador Fortran gfortran e especificando as bibliotecas LAPACK e BLAS

```sh
cmake .. -DCMAKE_Fortran_COMPILER=gfortran -DLAPACK_LIBRARIES="/usr/lib/liblapack.so.3" -DBLAS_LIBRARIES="/usr/lib/libblas.so.3"
```

#### 2. Usando o compilador Fortran Intel

```sh
cmake .. -DCMAKE_Fortran_COMPILER_ID=Intel
```

#### 3. Usando o compilador Fortran gfortran com configurações de Debug e desativando palavras-chave de threads

Esse passo só é recomendando caso você queira desenvolver para o MOPAC.

```sh
cmake -DCMAKE_Fortran_COMPILER=gfortran -DLAPACK_LIBRARIES="/usr/lib/liblapack.so.3" -DBLAS_LIBRARIES="/usr/lib/libblas.so.3" -DCMAKE_BUILD_TYPE=Debug -DTHREADS_KEYWORD=OFF ..
```
