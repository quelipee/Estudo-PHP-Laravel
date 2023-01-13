# **<center>ESTUDO SOBRE LARAVEL E PHP</center>**

## **Vantagens do laravel?**

<p>Por que laravel é um framework que utiliza a ferramenta mvc, que significa 
MODEL VIEW CONTROLLER, e é uma otima ferramenta para criar coisas na web </p>

<br>

## **Como criar um projeto laravel**

- <p>via composer</p>

````php
composer create-project laravel/laravel example-app
````

<br>

- <p>instalando o composer no laravel, e criando projeto via laravel</p>

````php
composer global require laravel/installer
 
laravel new example-app
````

<br>

## **Como inicializar um server via laravel**

````php
php artisan serve
````

<br>

## **Laravel pode servir como uma API**
<p>O laravel pode ser usado como uma API para suas outras aplicações,
como fornecer uma autenticação, e armazenamento/recuperação de dados para seu aplicativo,</p>

<br>

## **Laravel utiliza o metodo MVC**

<p>O metodo MVC, significa model view controller, a model onde faz as consultas
no banco de dados, e em contra partida a view vai ser onde o usuario vai poder
visualizar o resultado da sua aplicação, que foi solicitado pelo controller.</p>

<br>

### **Como ver as configurações do seu projeto**

- ver todos os arquivos dentro do mesmo:

```php
php artisan about
```
- ver uma parte especifica do seu projeto:

```php
php artisan about --only=environment
```
<br>

## **Criptografar um arquivo de ambiente:**

- comando:
````php
php artisan env:encrypt
````

- resultado:
````php
 Key ................................... base64:LSB4/YrVDQmoPgsMOxGQOuUNTKll+IZTM78lOiid0tE=
 Cipher ........................................................................ AES-256-CBC
 Encrypted file ........................................... C:\laravel\estudo\.env.encrypted
  ````

<p>A execução do comando env:encrypt criptografará seu arquivo .env e colocará o conteúdo criptografado em um arquivo .env.encrypted</p>

<br>

## **Criar link entre duas STORAGE:**
<p>Essa função é utilizada para vincular a pasta storage com a a pasta public</p>

````php
php artisan storage:link
````

## **FRONT END** 

<p>O laravel facilita para a utilização do php no front end</p>

````php
<div>
    @foreach ($users as $user)
        Hello, {{ $user->name }} <br />
    @endforeach
</div>
````

<p>Utilizando o @ podera utilizar algumas funções php no html que utiliza o modelo blade, como por exemplo o if:</p>

````php
<div>
    @if ($user)
        Hello world;
    @endif
</div>
````
<br>

## **Laravel Breeze**

<p>O laravel breeze é um recurso ja contruido do laravel que ja vem imprementado autenticacao, login
registro, redefinição de senha, verificação de email, entre outras funções que proporciona.
</p>

- Instalação do Breeze:

````php
composer require laravel/breeze --dev
````
<br>
<p>
Este comando publica as exibições de autenticação, rotas, controladores e outros recursos para seu aplicativo. O Laravel Breeze publica todo o seu código em seu aplicativo para que você tenha total controle e visibilidade sobre seus recursos e implementação.
</p>

````php
php artisan breeze:install
````
<br>

- <p>tela criada pelo breeze e suas funções,Ex: login, register e autenticação do usuario ao logar:</p>

![img_1.png](https://laravel.com/img/docs/breeze-register.png)

<br>

---
## **O que é middleware**

![middleware](https://lh3.googleusercontent.com/JAgK6v_olWVMXu5LVjTDZN5liFRhhbRNhJpyZx-VM--kfkfoq9UxaIJlfFwMPIZbfZzzWxSxQS0fXun1x7KWeLxQo_tob1OFRBTJQqeCl01lMT2Scyu1CkHGCoZ2qjDuK7hRvLr-)

<p>No ramo do TI, middleware é o software que serve como ponte de comunicação entre o sistema operacional e as funções de um aplicativo. Servidores de aplicativos, softwares de mensagem, bancos de dados e monitores de processamento de transação são alguns exemplos de middlewares.</p>

<br>

### Exemplos:

<p>Middleware é um tipo de software que atua como uma "ponte" entre duas partes de um sistema. Ele pode ser usado para filtrar informações, autenticar usuários, proteger contra ataques e muito mais. Por exemplo, imagine que você tem um jogo on-line que só pode ser jogado por pessoas com mais de 10 anos. O middleware pode verificar a idade do usuário antes de permitir que ele entre no jogo, assim só as pessoas com idade adequada podem jogar.<p/>

<br>

<p>Imagine que você quer ir brincar na rua, mas antes precisa perguntar se pode sair de casa. Seu pai é o middleware, ele vai verificar se você já fez sua lição de casa, se está vestindo roupas adequadas e se tem permissão para sair. Se tudo estiver certo, ele vai deixar você sair. Se alguma coisa estiver errada, ele vai pedir para você resolver antes de poder sair. Isso serve para garantir que as regras e as condições estabelecidas sejam seguidas e para proteger o sistema de possíveis problemas ou ameaças.<p/>

<br>

<p>Middleware é como um filtro que fica entre o usuário e o sistema. Ele verifica se o usuário tem permissão para acessar determinada página ou realizar uma determinada ação. Por exemplo, imagine que você tem um site de compras online e só quer deixar que os usuários logados façam compras. Então você pode criar um middleware que verifique se o usuário está logado antes de permitir que ele adicione um produto ao carrinho. Dessa forma, os usuários que não estão logados não conseguirão fazer compras, mesmo que tentem acessar a página de finalização de compra diretamente. Middleware é uma forma de proteger o sistema e garantir que as regras de acesso sejam seguidas.<p/>

<br>

## **EXEMPLO EM CODIGO**
<p>Dentro do método handle, você pode colocar a lógica de verificação de permissão de administrador. Por exemplo:<p/>

````php
public function handle($request, Closure $next)
{
    if (Auth::user()->is_admin) {
        return $next($request);
    }
    return redirect('/');
}
````

<p>Depois de criar o middleware, você precisa registrá-lo em app/Http/Kernel.php. Adicione o nome do middleware na propriedade $routeMiddleware.

Por fim, você pode usar o middleware na rota da página de gerenciamento de usuários, assim:<p/>


````php
Route::get('/admin/users', 'AdminController@index')->middleware('admin');
````

<p>Agora, quando um usuário tentar acessar a página de gerenciamento de usuários, o middleware verificará se ele tem permissão de administrador. Se tiver, o usuário será permitido acessar a página. Se não tiver, ele será redirecionado para a página inicial.<p/>

---

## **Middleware no laravel**

<p>Depois que a rota ou o método do controlador retornar uma resposta, a resposta viajará de volta para fora através do middleware da rota, dando ao aplicativo a chance de modificar ou examinar a resposta de saída.

Finalmente, uma vez que a resposta viaja de volta pelo middleware, o método handle do kernel HTTP retorna o objeto de resposta e o arquivo index.php chama o método send na resposta retornada. O método send envia o conteúdo da resposta para o navegador da Web do usuário. Terminamos nossa jornada por todo o ciclo de vida da solicitação do Laravel!</p>

<br>

---

## **Criando um 'Hello World' via rota**


### onde a mesma injenta uma função dentro da propria rota, e retorna a string 'Hello World'

````php
use Illuminate\Support\Facades\Route;
 
Route::get('/greeting', function () {
    return 'Hello World';
});
````

<br>

# **O Router permite cadastrar rotas que respondem a qualquer verbo HTTP:**

````php
Route::get($uri, $callback);
Route::post($uri, $callback);
Route::put($uri, $callback);
Route::patch($uri, $callback);
Route::delete($uri, $callback);
Route::options($uri, $callback);
````

- Metodo para usar todas as rotas HTTP:
````php
Route::any('/', function () {
    //
});
````
- Para usar 2 metodos especificos:
````php
Route::match(['get', 'post'], '/', function () {
    //
});
````

# **Utilizando rotas HTTP em forms no laravel:**
<p>Sempre quando utilizar o form no laravel, o desenvolvedor tem que utilizar
a funcao @csrf, para que quando for mandar o form nao de rejeição na sua solitacao.</p>

````php
<form method="POST" action="/profile">
    @csrf
    ...
</form>
````

<br>

# **Formas de redirecionar uma rota no laravel:**
````php
Route::redirect('/here', '/there');
````

- o redirect sempre retorna por padrao uma status, adicionando uma informação a mais no codigo vc pode personalizar o status para o desejavel:
````php
Route::redirect('/here', '/there',302);
````

- metodo para retornar o status padrao 301 da route:
````php
Route::permanentRedirect('/here', '/there');
````

<br>

### **Como redirecionar uma rota para uma view**

````php
Route::view('/welcome', 'welcome');
 
Route::view('/welcome', 'welcome', ['name' => 'Taylor']);
````

<br>

## **Ver todas as rodas usadas e o tipo:**

````php
php artisan route:list
````

<br>

<br>

## **Tests: Exemplo de como utilizar o phpunit com laravel**
````php
        //prepare
        $payload = [
            'title' => 'tirar o lixo',
            'description'=> 'nao esquecer de tirar o lixo'
        ];

        //act
        $result = $this->post('todos',$payload);

        //assert
        $result->assertStatus(201); //201 = created;
        $this->assertDatabaseHas('todos',['title'=>$payload['title'],
        'description'=>$payload['description']]);
````
<p>Nesse exmplo utilizamos uma variavel chamada $payload para fazer uma array com os mesmo
nomes que estou utilizando no database, para fazer a criação de um post no database, e para 
confirmar se o post foi criado utilizando o assertStatus com o codido 201 confirmando que foi criado, ja o assertDatabaseHas ele verifica se o item esta no database.</p>

<br>

## **O que é uma API**
---

<p>Uma API, ou Application Programming Interface, é uma maneira de dois sistemas se comunicarem e trocarem informações. Imagine que você quer pedir uma pizza pelo telefone, mas o telefone da pizzaria só fala em italiano, enquanto você fala apenas português. Para conseguir se comunicar, você precisa de um tradutor, que seria a API. Ela vai traduzir o que você fala para o idioma da pizzaria e, quando eles responderem, ela também vai traduzir para você. Assim, você consegue encomendar a sua pizza sem saber falar italiano. É assim que as APIs funcionam: elas ajudam os sistemas a se comunicarem e trocarem informações, mesmo que eles falem diferentes linguagens de programação.<p/>

!["api"](https://blog.cod3r.com.br/wp-content/uploads/2022/05/como-api-funciona.jpg)

<br>

## **HTTP**

<p>HTTP é como um correio. Quando você precisa enviar uma carta ou pacote para alguém, você escreve ou coloca o item dentro de uma caixa, cola um endereço no pacote e o leva para o correio. O correio então pega a caixa e a leva para o endereço no pacote.

Da mesma forma, quando você usa um computador para ver uma página na internet, você está enviando um pedido para ver a página para outro computador. O seu computador envia a solicitação através de algo chamado HTTP, que é como o correio da internet. O outro computador recebe a solicitação e envia a página de volta para o seu computador, e você pode vê-la.

Então, basicamente, o HTTP é uma forma de se comunicar e trocar informações entre computadores através da internet.<p/>

![HTTP](https://miro.medium.com/max/1400/0*sr8XF4ztxyBBWueS)

<br>

## **Exceptions**
---

<p>Exceptions são como sinais de alerta que indicam que algo deu errado em um programa. É como se fosse um sinal de emergência que diz: "Ei, algo aconteceu aqui e precisamos parar tudo e tratar isso!". Você pode criar suas próprias exceptions personalizadas para lidar com situações específicas em seu programa, como tentar acessar um arquivo que não existe ou tentar dividir um número por zero (que dá um erro muito sério!). Quando uma exception é lançada, o programa para de rodar e começa a procurar por uma maneira de lidar com ela. Isso é muito útil porque nos permite ter um controle melhor sobre o que acontece em nosso programa e como lidamos com problemas quando eles aparecem.<p/>

<br>

### **Outros exemplos sobre o que são exception!!!**

<p>Exceptions são erros que ocorrem em um programa. Elas são usadas para informar que algo deu errado e interromper o fluxo normal de execução do código. Por exemplo, imagine que você está fazendo uma divisão por zero. Isso geralmente não é permitido na matemática, então o programa pode lançar uma exceção para avisar que houve um erro e interromper a execução do código. Exceptions são úteis porque nos permitem tratar esses erros de forma mais organizada e evitar que o programa quebre completamente.<p/>

<br>

## **Exmplo de Exception Laravel em codigo!!**

<p>Exemplo de criação de uma exception no Laravel:<p/>

<p>Crie uma nova classe de exception em app/Exceptions:<p/>



````php
use Exception;

class MinhaException extends Exception
{
    //
}
````
Lançe a exception em algum lugar do seu código, por exemplo:

````php
if ($condicao) {
    throw new MinhaException('Mensagem da exception');
}
````
<p>Crie um manipulador de exceptions em app/Exceptions/Handler.php:<p/>

````php
public function render($request, Exception $exception)
{
    if ($exception instanceof MinhaException) {
        return response()->json(['mensagem' => $exception->getMessage()], 400);
    }

    return parent::render($request, $exception);
}
````
<p>Desta forma, todas as vezes que a exception MinhaException for lançada, o código acima tratará a exception e retornará uma resposta JSON com a mensagem da exception.<p/>

<br>

---
## **Exemplo de uso de exceção em PHP:**
<br>

````php
function dividir($dividendo, $divisor) {
  if ($divisor == 0) {
    throw new Exception("Não é possível dividir por zero");
  }
  return $dividendo / $divisor;
}

try {
  $resultado = dividir(10, 0);
} catch (Exception $e) {
  echo "Ocorreu um erro: " . $e->getMessage();
}
````
<p>Neste exemplo, a função "dividir" lança uma exceção quando o divisor é zero. Isso é capturado pelo bloco "try-catch" e a mensagem de erro é exibida para o usuário.<p/>

<br>

---

<br>

## **Usando Service em laravel**

<p>Para criar um service no Laravel 9, você pode seguir os seguintes passos:<p/>

<p>Crie uma pasta chamada "Services" dentro da pasta "app", se ainda não existir.<p/>

<p>Dentro da pasta "Services", crie um arquivo com o nome do service que você quer criar, por exemplo "UserService.php". Esse arquivo deve conter a classe do service, que pode ser definida da seguinte forma:<p/>

````php
<?php

namespace App\Services;

use Illuminate\Support\Facades\DB;

class UserService
{
    // métodos e atributos do service
}
````

<p>Dentro da classe UserService, você pode adicionar os métodos que deseja, por exemplo:<p/>

````php
public function getUsers()
{
    return DB::table('users')->get();
}

public function createUser($data)
{
    return DB::table('users')->insert($data);
}
````

<p>Para utilizar o service em outro lugar da aplicação, você pode injetá-lo como dependência, por exemplo em um controller:<p/>

````php
use App\Services\UserService;

class UserController extends Controller
{
    private $userService;

    public function __construct(UserService $userService)
    {
        $this->userService = $userService;
    }

    public function index()
    {
        $users = $this->userService->getUsers();

        return view('users.index', compact('users'));
    }
}
````

Em seu arquivo "app/Providers/AppServiceProvider.php", você pode registrar o service para ser injetado em qualquer lugar da aplicação, adicionando a seguinte linha no método "register":

````php
$this->app->singleton(UserService::class, function () {
    return new UserService();
});
````

<p>Dessa forma, toda vez que o service for injetado em algum lugar da aplicação, ele será instanciado apenas uma vez e reutilizado nas demais injeções.<p/>

<br>

---

<br>

## **Usando a função tooManyAttempts da classe RateLimiter**

````php
if (RateLimiter::tooManyAttempts($key, 5)) {
    // Número de tentativas excedido, impedir o acesso
} else {
    // Número de tentativas permitido, permitir o acesso
}
````

<p>Nesse exemplo, a função tooManyAttempts é chamada com uma chave $key e o número máximo de tentativas permitidas igual a 5. Se o número de tentativas tiver sido excedido, o código dentro do bloco if será executado. Caso contrário, o código dentro do bloco else será executado.<p/>

--- 

<br>
<br>

## **Gerenciamento de erros e exceções**

<p>PHP oferece vários mecanismos para lidar com erros e exceções, que podem ser usados ​​para garantir que seus aplicativos sejam robustos e seguros. O recurso mais comum é o uso de funções para tratar erros, como trigger_error() e set_error_handler().<p/>

<p>Além disso, o PHP também oferece suporte a exceções, que são eventos anormais que podem ser lançados e capturados em seu código. Utilizando exceções pode ajudá-lo a escrever códigos mais limpos e mais fáceis de ler, e tratar erros de maneira mais organizada.<p/>

<p>As exceções são lançadas usando a instrução throw e capturadas usando a instrução try-catch.<p/>

````php
try {
  // Código que pode lançar uma exceção
  if ($variavel === 0) {
    throw new Exception("Variavel é igual a zero");
  }
} catch (Exception $e) {
  echo $e->getMessage();
}
````

<p>Quando uma exceção é lançada, a execução do código é interrompida e o fluxo de execução é transferido para o primeiro bloco catch correspondente que está dentro do escopo. Dessa forma, é possível lidar com erros de maneira mais organizada e segura.<p/>

---
<br>

<p>Além disso, é uma boa prática criar classes de exceção personalizadas, onde você pode definir mensagens de erro específicas e níveis de erro para diferentes tipos de exceções. Isso pode tornar mais fácil para você controlar os erros no seu código e fornecer uma resposta adequada a cada erro.

Além disso, você também pode usar gerenciadores de exceções globais para lidar com exceções que não são capturadas em nenhum outro lugar do código. Isso pode ser útil para registrar erros críticos ou notificar os desenvolvedores sobre esses erros.

Além de gerenciamento de erros e exceções, é importante lembrar de sempre validar e limpar os dados de entrada do usuário. Isso é uma parte importante da segurança do seu aplicativo, pois ajuda a evitar ataques como injeção SQL e ataques XSS.

Isso é um breve resumo do gerenciamento de erros e exceções no PHP. Se você tiver alguma dúvida sobre esses tópicos ou quiser ver mais exemplos, não hesite em me perguntar.<p/>

<br>

## **Aqui estão alguns exemplos adicionais de como usar exceções no PHP:**

<br>

<p>Lançando uma exceção personalizada:<p/>

````php
class MeuErroException extends Exception {
    public function __construct($mensagem, $codigo = 0, Exception $anterior = null) {
        parent::__construct($mensagem, $codigo, $anterior);
    }
}

try {
    throw new MeuErroException('Aconteceu algo inesperado');
} catch (MeuErroException $e) {
    echo 'Erro: ' . $e->getMessage();
}

````

<p>Utilizando a classe Exception para gerenciar erros de sistema:<p/>

````php
try {
    if (!file_exists('arquivo.txt')) {
        throw new Exception("Arquivo não encontrado", 404);
    }
    // Continuar o processamento do arquivo
} catch (Exception $e) {
    echo 'Erro: ' . $e->getMessage() . ', código: ' . $e->getCode();
}
````

<br>

## **Função set_exception_handler()**

````php
function meuGerenciadorExcecoes($e) {
    // Personalizando o tratamento para exceções
    echo 'Erro: ' . $e->getMessage();
}
set_exception_handler('meuGerenciadorExcecoes');

throw new Exception('Testando meu gerenciador de exceções');
````
<p>A função set_exception_handler() é como um controle de erros no seu código, assim como um guardião que está sempre vigiando seu código para garantir que ele esteja funcionando corretamente. É como se você tivesse um botão de emergência no seu código e, quando algo inesperado acontece, ele pressiona esse botão e chama alguém para ajudá-lo a consertar o problema.<p/>

<p>A função set_exception_handler() é usada para dizer ao seu código para chamar uma função específica quando algo de errado acontece e uma exceção é lançada, essa função é chamada de 'manipulador de exceção'. Isso significa que, em vez de o código simplesmente parar de funcionar quando algo de errado acontece, ele chama essa função para tratar o problema, assim como se você chama um adulto quando você precisa de ajuda. Assim, a função pode tratar o erro de maneira adequada, mostrando uma mensagem de erro amigável ou registrando o erro para depuração.<p/>

<br>

## **Utilizando múltiplas camadas de tratamento de exceção:**

````php
function verificaValor($valor) {
    if ($valor < 0) {
        throw new Exception("Valor não pode ser menor que 0");
    }
    return $valor;
}

try {
    $resultado = verificaValor(-1);
} catch (Exception $e) {
    echo 'Erro: ' . $e->getMessage();
}
````
<p>Nesse exmplo estamos criando uma função simples que verifica se um valor é menor do que zero. Se for, uma exceção é lançada e capturada no bloco catch correspondente, mostrando uma mensagem de erro personalizada.<p/>

<br>

## **Exemplo de uma função que valida se uma string é um endereço de e-mail válido usando expressão regular no PHP:**

````php
function validaEmail($email) {
  // Padrão de expressão regular para verificar o formato do endereço de e-mail
  $padrao = '/^[a-zA-Z0-9.!#$%&’*+/=?^_`{|}~-]+@[a-zA-Z0-9-]+(?:\.[a-zA-Z0-9-]+)*$/';
  
  if (!preg_match($padrao, $email)) {
    throw new Exception("Endereço de e-mail inválido");
  }
  
  // se chegou aqui é porque o email é válido
  return true;
}
````

<p>A função usa a função preg_match() do PHP para verificar se a string passada como argumento corresponde ao padrão de expressão regular. O padrão de expressão regular é uma combinação de caracteres que representa o formato esperado para um endereço de e-mail.
Se o email não bater com o formato, a função lança uma exceção chamada "Endereço de e-mail inválido" e se estiver correto retorna true.

Tenha em mente que essa validação usando expressão regular é uma forma simples para verificar o formato do endereço de e-mail, mas não garante 100% que o endereço seja válido. Outras verificações adicionais, como checar se o domínio é válido e se o endereço existe realmente, podem ser necessárias para garantir a precisão da validação.<p/>

<br>

## **Exemplo de uma função que valida se uma string é um endereço de e-mail válido usando expressão regular no PHP**

````php
function validaEmail($email) {
    // Padrão de expressão regular para verificar o formato do endereço de e-mail
    $padrao = '/^[a-zA-Z0-9.!#$%&’*+\/=?^_`{|}~-]+@[a-zA-Z0-9-]+(?:\.[a-zA-Z0-9-]+)*$/';;
    
    try {
        if (!preg_match($padrao, $email)) 
        {
            throw new Exception("Endereço de e-mail inválido");
        }
    } catch (Exception $e) {
        echo "message: " . $e->getMessage();
    }
    // se chegou aqui é porque o email é válido
    return true;
  }

validaEmail("felipemateus@email.com");
````

<p>A função usa a função preg_match() do PHP para verificar se a string passada como argumento corresponde ao padrão de expressão regular. O padrão de expressão regular é uma combinação de caracteres que representa o formato esperado para um endereço de e-mail.
Se o email não bater com o formato, a função lança uma exceção chamada "Endereço de e-mail inválido" e se estiver correto retorna true.

Tenha em mente que essa validação usando expressão regular é uma forma simples para verificar o formato do endereço de e-mail, mas não garante 100% que o endereço seja válido. Outras verificações adicionais, como checar se o domínio é válido e se o endereço existe realmente, podem ser necessárias para garantir a precisão da validação.<p/>

---

<br>

### **Exemplo de Exception com banco de dados** 
<p>Crie uma classe para se conectar a um banco de dados que tem métodos para abrir e fechar conexões. Utilize exceções para garantir que as conexões sejam abertas e fechadas corretamente e para tratar erros de conexão com o banco de dados.<p/>

````php
class Database
{
    public $conn;

    public function databaseValidation()
    {
        $this->conn = mysqli_connect('localhost','root','1234','projeto');
        if(!$this->conn)
        {
            echo "error " . mysqli_connect_error($this->conn);
            exit;
        }
        return $this->conn;
    }

    public function abrir()
    {
        try {
            if(!$this->conn)
            {
                throw new Exception();
            }
        } catch (Exception $e) {
            echo "message: " . $e->getMessage() . "\n";
            exit;
        }
        return true;
    }

    public function fechar()
    {
        try {
            if (!$this->conn) {
                throw new Exception("error ao tentar fechar a conecção!!!\n");
            }
        } catch (Exception $e) {
            echo "message: " . $e->getMessage();
            exit;
        }
        mysqli_close($this->conn);
        echo "conecção fechada!!!";
    }
}

$db = new Database();
$db->databaseValidation();
print_r($db->abrir());
$db->fechar();
````

<br>

## **Atividade sobre Excepetions**

<p>Escreva uma função que valida endereços de e-mail.
Use uma exceção personalizada para lidar com endereços de e-mail inválidos (por exemplo, "Endereço de e-mail inválido").<p/>

````php
class Email
{
    protected $expressoes = "/^[a-zA-Z0-9._%-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,6}$/";
    public function validEmail($email)
    {
        return preg_match($this->expressoes, $email);
    }
}

try {
    $e = new Email();
    if ($e->validEmail('felipe@gmail.com'))
    {
        echo "email valido!!!\n";
    }else{
        throw new Exception("email nao é valido!!!\n");
    }
}catch (Exception $e)
{
    echo "message: " . $e->getMessage();
}
````

---

<br>

## **Arquivos em php**

<p>Trabalhar com arquivos no PHP inclui várias operações, como abertura, leitura, escrita e fechamento de arquivos. A biblioteca padrão do PHP fornece várias funções para realizar essas tarefas, como fopen(), fread(), fwrite() e fclose().<p/>

<p>Aqui está um exemplo de como abrir, ler e fechar um arquivo usando essas funções:<p/>

````php
<?php
$file = fopen("example.txt", "r");
$contents = fread($file, filesize("example.txt"));
fclose($file);

echo $contents;
?>
````

<p>Você também pode usar a função file_get_contents() para ler o conteúdo de um arquivo em uma única linha de código.<p/>

````php
<?php
$contents = file_get_contents("example.txt");
echo $contents;
?>
````

<p>Para escrever em um arquivo, você pode usar a função fwrite().<p/>

````php
<?php
$file = fopen("example.txt", "w");
$text = "Some text to be written in file.";
fwrite($file, $text);
fclose($file);
?>
````

<p>Além disso, existem funções para manipular arquivos CSV e ZIP como, por exemplo, fgetcsv(), str_getcsv() para lidar com arquivos csv e zip_open(), zip_entry_open() entre outros para lidar com arquivos zip.<p/>

<br>

---

### **Manipulando arquivos CSV:**

````php
// Abrindo o arquivo CSV
$file = fopen("dados.csv", "r");

// Lendo cada linha do arquivo e convertendo-a em um array
while (($data = fgetcsv($file)) !== FALSE) {
    // Processando os dados do array
    print_r($data);
}

// Fechando o arquivo
fclose($file);
````

### **Manipulando arquivos ZIP:**

````php
$zip = zip_open("arquivos.zip");

// Iterando sobre os arquivos dentro do arquivo zip
while ($zip_entry = zip_read($zip)) {
    // Abrindo o arquivo atual
    zip_entry_open($zip, $zip_entry);

    // Lendo o conteúdo do arquivo
    $contents = zip_entry_read($zip_entry);
    echo $contents;

    // Fechando o arquivo atual
    zip_entry_close($zip_entry);
}

// Fechando o arquivo zip
zip_close($zip);
````
<p>Esses são apenas alguns exemplos básicos de como lidar com arquivos CSV e ZIP no PHP. Há muitos outros recursos e funções disponíveis para lidar com esses tipos de arquivos de maneira mais avançada. Eu recomendo ler a documentação do PHP para obter mais informações sobre essas funções e como usá-las.<p/>

<br>

````php
<?php
    $file = fopen("novo_arquivo.txt", "w") or die("Não foi possível criar o arquivo!");
    fwrite($file, "Conteúdo do arquivo");
    fclose($file);
    echo "Arquivo criado com sucesso!";
?>
````
<p>Este exemplo usa a função fopen() para criar um novo arquivo chamado "novo_arquivo.txt" no modo de escrita (w). É recomendável sempre tratar erros como esse exemplo usando "or die" , para caso algo dê errado.<p/>

É importante notar que, ao criar um arquivo, você precisa ter permissão de escrita no diretório onde o arquivo será criado. Caso contrário, a função fopen() retornará um erro e o arquivo não será criado.<p/>

<p>Existe várias outras formas de criar arquivos, como por exemplo, usando a função file_put_contents() ou usando a biblioteca SPL (Standard PHP Library) para criar<p/>

---
<br>

## **Segurança**

<p>Aprender a garantir a segurança de seus aplicativos PHP, incluindo assuntos como validação de entrada de dados, criptografia e autenticação de usuários.<p/>

<p>A segurança em aplicativos PHP é crucial para garantir que seus dados e usuários estejam protegidos contra ataques como injeção de SQL, cross-site scripting (XSS) e cross-site request forgery (CSRF).<p/>

<p>Uma das principais formas de garantir a segurança é através da validação de entrada de dados. Isso inclui verificar se os dados fornecidos pelo usuário estão no formato esperado e se estão dentro dos limites aceitáveis. Você pode usar funções built-in do PHP como filter_var() e filter_input() para validar dados, ou usar bibliotecas como o Respect/Validation.<p/>

<p>Outra forma de garantir a segurança é através da criptografia de dados sensíveis. O PHP possui uma série de funções built-in para criptografar dados, como md5(), sha1() e hash(). É importante escolher um algoritmo de criptografia seguro, como o bcrypt ou argon2, e nunca armazenar senhas em texto claro.<p/>

<p>Por fim, a autenticação de usuários é outra forma de garantir a segurança de seus aplicativos PHP. Isso inclui verificar se o usuário é quem ele diz ser através de mecanismos como login e senha. É importante usar funções built-in do PHP como password_hash() e password_verify() para armazenar e verificar senhas de maneira segura.<p/>

<p>Para proteger seus aplicativos de outras ameaças de segurança, é importante estar sempre atualizado com as últimas vulnerabilidades e corrigi-las rapidamente, usar uma configuração segura e usar bibliotecas e frameworks seguros.<p/>

<br>

<p>Validação de entrada de dados é importante para garantir que os dados enviados pelo usuário sejam válidos e seguros. Uma forma de fazer isso é usando funções de validação nativas do PHP, como filter_var() ou preg_match().<p/>

### **Exemplo de validação de endereço de email:**

````php
if(filter_var($email, FILTER_VALIDATE_EMAIL)) {
    // processar email
} else {
    // email inválido
}
````
### **Outra forma de validação é usando expressões regulares, como:**

````php
if (preg_match("/^[a-zA-Z0-9._%-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,4}$/", $email)) {
    // processar email
} else {
    // email inválido
}
````

<p>Para criptografia, o PHP oferece várias funções, como md5(), sha1() e hash(). Por exemplo, para criptografar uma senha antes de armazená-la em um banco de dados:<p/>

````php
$senha_criptografada = password_hash($senha, PASSWORD_DEFAULT);
````

<p>Autenticação de usuários é o processo de garantir que um usuário seja quem ele diz ser. Isso pode ser feito usando sessões e cookies, para armazenar informações de usuário autenticado e verificar se ele tem acesso às páginas restritas.<p/>

````php
session_start();
if(isset($_SESSION['usuario_logado']) && $_SESSION['usuario_logado'] == true){
    // usuário está logado e tem acesso à página
}else{
    // usuário não está logado e não tem acesso à página
}
````

Esses são apenas alguns exemplos, e há muitos outros recursos disponíveis para garantir a segurança de aplicativos PHP.

--- 
<br>

## **Criptografia de senhas**

<p>bcrypt, scrypt e Argon2 são algoritmos de criptografia de senha que foram projetados especificamente para armazenar senhas de maneira segura. Eles são mais seguros do que as funções md5 e sha1, pois incluem características adicionais para tornar o processo de quebra de senha mais difícil.<p/>

<br>

## **bcrypt**
<p>bcrypt é um algoritmo de criptografia de fluxo de chave simétrica baseado em Blowfish. Ele usa um salt aleatório para tornar cada hash único, mesmo quando as senhas são as mesmas. Ele também usa um parâmetro de custo, que controla quantas iterações são necessárias para calcular o hash, tornando o processo de quebra de senha mais lento. Exemplo:<p/>

````php
$options = [
    'cost' => 12,
];
$password = "mypassword";
$password_hash = password_hash($password, PASSWORD_BCRYPT, $options);
````
<br>

## **scrypt**
<p>scrypt é um algoritmo de criptografia de senha baseado em chave simétrica que tem como objetivo tornar o processo de quebra de senha mais difícil, aumentando o uso de memória. Ele usa salt aleatório, e também usa parâmetros de custo e tamanho de bloco para tornar o processo de quebra de senha mais lento. Exemplo:<p/>

````php
$options = [
    'cost' => 15,
    'memory_cost' => 1<<17,
    'threads' => 3,
];
$password = "mypassword";
$password_hash = password_hash($password, PASSWORD_ARGON2I, $options);
````

<p>Argon2 é outro algoritmo de criptografia de senha baseado em chave simétrica, mas ele é considerado mais seguro do que bcrypt e scrypt. Ele também usa salt aleatório, e usa parâmetros de custo e tipo(Argon2i ou Argon2d) para tornar o processo de quebra de senha mais lento.<p/>

<br>

<p>O número ideal para o parâmetro "cost" varia de acordo com o hardware e a necessidade de segurança do sistema. Em geral, um valor de custo de 12 já é considerado seguro e razoavelmente rápido para a maioria dos sistemas atuais. No entanto, dependendo do seu sistema e do quão crítica é a segurança das senhas, você pode aumentar esse valor.

É importante avaliar a performance de seu sistema com diferentes valores de custo. Além disso, é importante monitorar a evolução da tecnologia e ajustar o valor de custo de tempos em tempos, para garantir a segurança da senha.

Além disso, é recomendado usar funções de verificação como password_verify() para comparar a senha digitada com o hash armazenado no banco de dados. Isso é importante para garantir a segurança da senha, pois evita a exposição de informações confidenciais.<p/>

---
<br>

## **Um exemplo de como usar password_verify()**

````php
$password = 'mypassword';
$hashed_password = Hash::make($password);

// Salva o hash criptografado no banco de dados

$password_to_check = 'mypassword';
if (password_verify($password_to_check, $hashed_password)) {
    // As senhas correspondem...
} else {
    // As senhas não correspondem...
}
````

<p>Neste exemplo, a primeira linha criptografa a senha fornecida e armazena o hash criptografado na variável $hashed_password. Em seguida, uma senha é fornecida para ser verificada ( $password_to_check ) e comparada com o hash armazenado ( $hashed_password ). Se as senhas corresponderem, a condição dentro do if será executada. Caso contrário, a condição no else será executada.<p/>

<p>Não armazene a senha em texto claro. Ao invés disso, armazene o hash da senha no banco de dados e use a função password_verify() para comparar a senha digitada com o hash armazenado.<p/>