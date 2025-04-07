### Moodle 4.5.3 pelo XAMPP

# 1 DOWLOAD XAMPP
- Fazer download do XAMPP: [https://www.apachefriends.org/pt_br/index.html](https://www.apachefriends.org/pt_br/index.html)
- Certificar-se de que a versão baixada contém o PHP entre 8.1 e 8.3.

# 2 PHP – configurando variáveis de ambiente
- No menu iniciar do Windows, digite “variáveis de ambiente” na barra de pesquisa.
- Clique em “Editar as variáveis de ambiente do sistema”.
- Na janela “Propriedades do sistema”, clique em “Variáveis de Ambiente...” no canto inferior direito.

  !(https://raw.githubusercontent.com/KarolDegan/Imagens/refs/heads/main/Imagens/Imagem1.png)

- Na seção “Variáveis de usuário”, localize e selecione a variável “Path”.
- Clique em “Editar” para modificar a variável.
- Clique em “Novo”.
- O caminho a ser adicionado deve apontar para o diretório onde o arquivo executável do PHP (php.exe) está localizado. Para o XAMPP, o caminho será geralmente algo como: `C:\xampp\php`.
- Clique em “OK” em todas as janelas para salvar as alterações.
- Abra o Prompt de Comando (cmd).
- Navegue até o diretório onde o PHP está localizado no XAMPP: 
  ```bash
  cd C:\xampp\php
  
- Para conferir se o PHP está funcionando corretamente, execute o comando:
    ```bash 
    php -v

# 3 Atualização MariaDB
- Faça o download da versão 10.6.21 (ou a versão 10.6 mais próxima) do MariaDB no formato ZIP.
- Interrompa a execução do XAMPP.
- Renomeie o arquivo `mysql` do diretório `xampp/` para `mysql-old`.
- Extraia a pasta do MariaDB para o diretório `xampp/`.
- Renomeie a pasta extraída para `mysql`.
- Copie os arquivos `mysql_installservice.bat`, `mysql_uninstallservice.bat` e `resetroot.bat` de `xampp/mysql-old` para `xampp/mysql`.
- Copie as pastas `backup` e `share` de `xampp/mysql-old` para `xampp/mysql`.
- Entre em `xampp/mysql-old/bin` e copie o arquivo `my.ini` para `xampp/mysql/bin`.
- Crie uma pasta com o nome “data” dentro do diretório `xampp/mysql` (esta pasta estará vazia inicialmente).
- Copie a pasta `xampp/mysql/data` para as pastas `mysql`, `performance_schema`, `phpmyadmin` e `test` presentes em `xampp/mysql-old/backup`.
- Execute o XAMPP.

# 4 Download do Moodle
- Entre na página: [https://download.moodle.org/releases/latest/](https://download.moodle.org/releases/latest/)
- Faça download da versão ZIP do Moodle 4.5.3.
- Extraia o Moodle para `xampp/htdocs`.

# 5 Configurações do PHP
- Vá até o diretório do PHP dentro do XAMPP: `xampp/php`.
- Abra `php.ini` em um bloco de notas ou outro editor de texto.
- Use a função de pesquisa (Ctrl + F) no editor de texto para procurar as extensões que estarão em um formato: `;extension=iconv`.

As extensões a serem descomentadas:
1. iconv
2. mbstring
3. curl
4. openssl
5. tokenizer
6. ctype
7. zlib
8. simplexml
9. spl
10. pcre
11. dom
12. xml
13. xmlreader
14. json
15. hash
16. fileinfo
17. exif
18. zip
19. gd
20. intl
21. sodium
22. soap

- Retire o “;” (descomente) de todas as extensões.
- Salve o arquivo `php.ini`.
- Reinicie o XAMPP.

# 6 Configurando Banco de Dados
- Abra o XAMPP.
- No painel de controle do XAMPP, clique em "Start" ao lado do MySQL para iniciar o servidor de banco de dados MySQL.
- Após o MySQL iniciar, clique em "Admin" na linha do MySQL. Isso abrirá o phpMyAdmin no seu navegador.

## Criar Banco de Dados:
- No phpMyAdmin, clique em "Novo" (no canto superior esquerdo).
- Crie um banco chamado “moodle”, com a Collation: “utf8mb4_unicode_ci”.

## Criar usuário admin:
- Com o banco de dados `moodle` selecionado, vá até a aba “Privilégios” no menu superior e clique em “Adicionar conta de usuário”.
- Dê um nome para o usuário e coloque o Nome do Host como `localhost`.
- Selecione a opção “conceder todos os privilégios no banco de dados moodle”.
- Clique em “executar” no campo superior esquerdo.
- Mantenha os privilégios específicos do banco de dados.

## Criando o `moodleuser`:
- Siga as instruções novamente para o `moodleuser`, mas modifique as configurações de “Privilégios específicos de banco de dados”:
- SELECT
- INSERT
- UPDATE
- DELETE
- CREATE
- CREATE TEMPORARY TABLES
- DROP
- INDEX
- ALTER

- Clique em "executar".

# 7 Alterando arquivo `config.php`
- Vá até o diretório `xampp/htdocs/moodle` e abra o arquivo “config.php” no editor de código de sua preferência:
```php
$CFG->dbtype    = 'mariadb';
$CFG->dblibrary = 'native';
$CFG->dbhost    = 'localhost';
$CFG->dbname    = 'moodle';
$CFG->dbuser    = 'moodleuser';
$CFG->dbpass    = 'yourpassword';
$CFG->prefix    = 'mdl_';
```

# 8 Configurando Moodle
- No seu navegador, digite: localhost/moodle
- Siga as instruções.
