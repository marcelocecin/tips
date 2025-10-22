# Technical Tips & Guides

Este repositório contém dicas técnicas e guias de configuração para desenvolvimento.

> **Nota:** Alguns destes procedimentos são de versões antigas de software e podem precisar de adaptações para sistemas modernos.

## Índice

- [Conversão de Certificados .p12 (Mac para Windows)](#conversão-de-certificados-p12-mac-para-windows)
- [Instalação do Alchemy Toolkit no Cygwin (Windows 7)](#instalação-do-alchemy-toolkit-no-cygwin-windows-7)

---

## Conversão de Certificados .p12 (Mac para Windows)

Este guia mostra como converter certificados .p12 exportados do Mac para uso no Windows.

### Pré-requisitos
- OpenSSL instalado no Windows
- Acesso ao certificado developer.cer
- Arquivo mac.p12 exportado do Keychain (Mac)

### Passos

1. **(Mac)** Download e instalação do `developer.cer`

2. **(Mac)** Exportar `mac.p12` através do Keychain Access

3. **(Win)** Download e instalação do `developer.cer`

4. **(Win)** Converter o certificado DER para PEM:
   ```bash
   openssl x509 -in developer.cer -inform DER -out developer.pem -outform PEM
   ```

5. **(Win)** Extrair a chave privada do arquivo Mac:
   ```bash
   openssl pkcs12 -nocerts -in mac.p12 -out mac.pem
   ```

6. **(Win)** Editar `mac.pem` no Notepad e salvar apenas a chave privada como `mac.key`

7. **(Win)** Criar o arquivo `win.p12` final:
   ```bash
   openssl pkcs12 -export -inkey mac.key -in developer.pem -out win.p12
   ```

---

## Instalação do Alchemy Toolkit no Cygwin (Windows 7)

Guia para configurar o Alchemy Toolkit da Adobe para compilar código C/C++ para SWC no Cygwin.

### Especificações Testadas
- **SO:** Windows 7 64-bits
- **Cygwin:** 1.7.9-1
- **Java JDK:** 1.6.0_23
- **Alchemy:** p1_121008
- **Flex SDK:** 3.2.0.3958

### Pré-requisitos

Antes de começar, você precisa ter:
- Java JDK instalado
- Acesso para download do Alchemy (Adobe Labs)
- Acesso para download do Flex SDK 3.2 (Adobe Opensource)

### Instalação Passo a Passo

1. **Instalar o Cygwin** com os seguintes pacotes:
   - `perl`
   - `zip` (categoria: archive)
   - `gcc/g++` (categoria: dev)

2. **Verificar instalação do Java**
   - Certifique-se de que o Java JDK está instalado

3. **Download do Alchemy** no Adobe Labs

4. **Download do Flex SDK 3.2** no Adobe Opensource

5. **Extrair os arquivos:**
   - Alchemy para: `c:\cygwin\home\<USER>\alchemy\`
   - Flex SDK para: `c:\cygwin\home\<USER>\flex\`

6. **Copiar executáveis Java para o Cygwin:**
   ```
   Copiar de: c:\program files (x86)\java\jdk\bin\
   - java.exe
   - javac.exe

   Para: c:\cygwin\bin\
   ```

7. **Configurar FLEX_HOME:**

   Abrir `c:\cygwin\home\<USER>\.bashrc` e adicionar:
   ```bash
   export FLEX_HOME=/home/<USER>/flex/bin
   ```

8. **Configurar o Alchemy:**

   Abrir `cygwin.exe` e executar:
   ```bash
   cd alchemy
   ./config
   exit
   ```

9. **Configurar ADL:**

   Abrir `c:\cygwin\home\<USER>\alchemy\alchemy-setup` e adicionar:
   ```bash
   export ADL=/home/<USER>/flex/adl.exe
   ```

10. **Configurar variáveis de ambiente no .bashrc:**

    Abrir `c:\cygwin\home\<USER>\.bashrc` e adicionar:
    ```bash
    export ALCHEMY_HOME=/home/<USER>/alchemy
    source /home/<USER>/alchemy/alchemy-setup
    PATH=$ALCHEMY_HOME/achacks:/home/<USER>/flex/bin:$PATH
    export PATH
    ```

11. **Corrigir script hacks.pl:**

    Abrir `c:\cygwin\home\<USER>\alchemy\achacks\hacks.pl` e alterar:
    ```perl
    # DE:
    if(`uname` =~ /CYGWIN/)

    # PARA:
    if(`/bin/uname` =~ /CYGWIN/)
    ```

12. **Configurar links simbólicos e testar:**

    Abrir `cygwin.exe` e executar:
    ```bash
    cd alchemy
    ln -s llvm-stub llvm-stub.exe
    alc-on; which gcc
    gcc stringecho.c -O3 -Wall -swc -o stringecho.swc
    ```

13. **Verificar instalação:**

    Confirmar que o arquivo foi criado em:
    ```
    c:\cygwin\home\<USER>\alchemy\samples\stringecho\stringecho.swc
    ```

### Troubleshooting

- Certifique-se de substituir `<USER>` pelo seu nome de usuário real
- Verifique se todas as variáveis de ambiente foram configuradas corretamente
- Reinicie o Cygwin após modificar o `.bashrc`

---

## Contribuindo

Sinta-se à vontade para adicionar mais dicas técnicas ou atualizar procedimentos existentes através de pull requests.

## Licença

Este repositório contém documentação e guias técnicos de uso livre.
