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
 Key ....................................................................... base64:YOURKEY=
 Cipher ............................................................................. Cipher
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

### No Laravel, existem alguns middlewares pré-definidos que você pode usar para implementar certas funcionalidades em sua aplicação. Alguns dos middlewares pré-definidos incluem:

- <p>web: Este middleware é aplicado a todas as rotas que precisam de suporte para sessão e autenticação.<p/>

- <p>api: Este middleware é aplicado a todas as rotas que precisam de suporte para autenticação e tokens de acesso.<p/>

- <p>auth: Este middleware é usado para proteger rotas que precisam de autenticação. Ele verifica se o usuário está autenticado e, se não estiver, redireciona-o para a tela de login.<p/>

- <p>guest: Este middleware é usado para proteger rotas que só devem ser acessadas por usuários não autenticados. Ele verifica se o usuário está autenticado e, se estiver, redireciona-o para a home page ou outra rota específica.<p/>

- <p>verified: Este middleware é usado para proteger rotas que só devem ser acessadas por usuários que já verificaram seu endereço de e-mail.<p/>

- <p>throttle: Este middleware é usado para limitar o número de solicitações que um usuário ou IP pode fazer dentro de um determinado período de tempo.<p/>

- <p>Esses são apenas alguns exemplos dos middlewares pré-definidos que estão disponíveis no Laravel, existem muitos outros que você pode usar dependendo das necessidades da sua aplicação.<p/>

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

--- 

<br>

## **Require_once**

<br>require_once é uma instrução no PHP que é usada para incluir e executar um arquivo em outro arquivo. Ele é semelhante a require, mas tem a adição de que ele só incluirá o arquivo uma vez, mesmo que ele seja incluído várias vezes.<p/>

<br>Quando você usa require_once em um arquivo, o PHP verifica se o arquivo já foi incluído. Se ele já foi incluído, o PHP não o incluirá novamente e seguirá com a execução do código. Se ele ainda não foi incluído, o PHP incluirá o arquivo e executará o código nele. Isso é útil quando você tem vários arquivos que precisam ser incluídos em vários lugares, mas você não quer incluí-los várias vezes, pois isso poderia causar problemas de conflito de funções ou variáveis.<p/>

<p>É importante notar que, se o arquivo não for encontrado, o PHP lançará uma exceção "PHP Fatal error: require_once(): Failed opening required" e interrompera a execução do script.<p/>

---

<br>

## **Funções sobre a api do twitter**

````
"statuses/update": permite postar um novo tweet.
"statuses/mentions_timeline": retorna tweets que mencionam o usuário autenticado.
"statuses/user_timeline": retorna tweets publicados pelo usuário especificado.
"users/show": retorna informações do perfil de um usuário específico.
"direct_messages/events/list": retorna mensagens diretas enviadas e recebidas pelo usuário autenticado.
"friendships/lookup": retorna dados de relacionamento entre usuários específicos.
"friends/ids": retorna os IDs dos amigos de um usuário específico.
````

<p>Essas são apenas algumas das opções disponíveis. A documentação da API do Twitter fornece uma lista completa de todos os endpoints disponíveis, bem como as informações necessárias para usá-los.<p/>

### **Exemplo de uma api onde busca os 10 tweets recentes da time line**
````php
require_once __DIR__ . "/vendor/autoload.php";
use Abraham\TwitterOAuth\TwitterOAuth;

$api_key =  'YOUR API KEY';
$api_key_secret = 'YOUR API KEY SECRET';
$token = 'YOUR TOKEN';
$token_secret = 'YOUR TOKEN SECRET';
define('CONSUMER_KEY',$api_key);
define('CONSUMER_SECRET',$api_key_secret);
define('ACCESS_TOKEN',$token);
define('ACCESS_TOKEN_SECRET',$token_secret);

$conn = new TwitterOAuth(CONSUMER_KEY, CONSUMER_SECRET, ACCESS_TOKEN, ACCESS_TOKEN_SECRET);
$user_timeline = $conn->get("statuses/home_timeline", ["count" => 10]);//ver os ultimos tweets da time line
foreach ($user_timeline as $tweet) {
    echo "nome do usuario: " . $tweet->user->name . $tweet->text . "\n";
}
````
### **Saida**
!['twitter api'](./storage/twitterapi.png)

---

## **Enums**

Em PHP Laravel, um Enum (ou enumeração) é um conjunto de constantes nomeadas que representam valores possíveis para um determinado tipo de dados. Em outras palavras, um Enum permite que você defina um conjunto limitado de valores que um atributo pode ter.

Por exemplo, você pode criar um Enum para representar os dias da semana, onde cada dia é uma constante nomeada com um valor inteiro associado:

````php
<?php

namespace App\Enums;

class Weekday {
  const MONDAY = 1;
  const TUESDAY = 2;
  const WEDNESDAY = 3;
  const THURSDAY = 4;
  const FRIDAY = 5;
  const SATURDAY = 6;
  const SUNDAY = 7;
}
````

Em seguida, você pode usar essa enumeração em outros lugares do seu código para 
representar dias da semana, como em um objeto DTO, em um modelo Eloquent ou em uma 
tabela do banco de dados.

Os Enums podem ajudar a tornar o seu código mais legível e menos propenso a erros, 
pois limitam o conjunto de valores que um atributo pode ter.


### **Outros exemplos sobre Enums**

Em PHP Laravel, um enum é um tipo de classe que representa um conjunto finito de 
valores possíveis. É semelhante a um conjunto de constantes nomeadas, em que cada 
constante tem um valor associado. No entanto, os enums são geralmente mais fáceis de 
usar e manter do que as constantes nomeadas. Isso ocorre porque os enums permitem que você defina um conjunto predefinido de valores possíveis, e também oferecem métodos úteis para trabalhar com esses valores, como a verificação se um valor específico está presente no conjunto, ou a obtenção de uma lista de todos os valores possíveis.

Por exemplo, um enum de cores pode ser definido como:


````php
enum Color {
RED,
GREEN,
BLUE
}
````
A partir daí, você pode usar os valores definidos em qualquer lugar em que precise 
especificar uma cor, como em uma variável ou em um parâmetro de função. Além disso, 
você pode usar métodos do enum, como Color::RED() para obter o valor correspondente à 
constante nomeada. Isso torna o código mais fácil de ler e entender, além de reduzir 
o risco de erros de digitação em constantes nomeadas.

---

## **$casts**

Em Laravel, a propriedade $casts em um modelo é usada para especificar como as 
colunas do banco de dados devem ser convertidas para tipos específicos ao serem 
atribuídas aos atributos do modelo.

Por exemplo, se você tem uma coluna chamada is_admin que é do tipo boolean no 
banco de dados, mas deseja acessá-la como um valor booleano em seu modelo, você 
pode especificar a conversão no $casts da seguinte maneira:


````php
protected $casts = [
'is_admin' => 'boolean',
];
````
Isso permite que você acesse o valor da coluna como um booleano em vez de uma string, 
por exemplo:



````php
if ($user->is_admin) {
// ...
}
````
Os tipos suportados para conversão incluem: integer, real, float, double, decimal:<digits>, string, boolean, object, array, collection, date, datetime, timestamp.

Além disso, você também pode especificar uma classe de casting personalizada que implementa a interface Illuminate\Contracts\Database\Eloquent\CastsAttributes, permitindo que você implemente uma lógica personalizada de conversão.

---

### **Tap**

O método tap é uma função do Laravel que permite você executar uma ação em um 
objeto sem alterar o seu estado. Ela recebe dois parâmetros: o objeto que você 
quer "tampar" e uma função que vai executar a ação desejada no objeto.

Por exemplo, imagine que você tem um objeto $user e quer mudar o seu nome para 
"Fulano". Em vez de fazer isso assim:



````php
$user->name = "Fulano";
````
Você pode usar o tap para executar a ação e continuar com o objeto original 
sem precisar armazenar o resultado em uma nova variável:



````php
tap($user, function ($user) {
$user->name = "Fulano";
});
````
Essa função é especialmente útil em cadeias de métodos, onde você quer executar 
uma ação em um objeto antes de passá-lo para o próximo método.

<br>

---

## **Function Static**

<p>Uma função estática em PHP é uma função que pode ser chamada sem precisar criar uma instância da classe à qual ela pertence.

Normalmente, quando você quer usar uma função que foi definida em uma classe, primeiro precisa criar uma instância dessa classe e, em seguida, chamar a função usando essa instância.

Mas com uma função estática, você pode chamar a função diretamente, sem precisar criar uma instância da classe. É como uma função global que está vinculada a uma classe específica.

Por exemplo, se você tiver uma classe chamada Exemplo, com uma função estática chamada funcStatica, você pode chamar essa função assim: Exemplo::funcStatica();.</p>

<br>

### **Outra exemplo sobre Function Static**

<p>Uma função estática, em PHP, é uma função que pode ser chamada sem precisar criar um objeto da classe em que ela está definida. Ou seja, ela pertence à classe e não a uma instância da classe.

Diferentemente das funções comuns, as funções estáticas não podem acessar propriedades e métodos não estáticos da classe. Além disso, elas não têm acesso ao $this, que é uma referência ao objeto atual da classe.

Para chamá-las, basta utilizar o nome da classe seguido pelo nome da função. Por exemplo, se você tem uma classe chamada Calculadora com uma função estática chamada soma, você pode chamá-la da seguinte forma: Calculadora::soma(2, 3).</p>

---

## **OQUE É DTO**

<p>DTO é uma sigla em inglês para Data Transfer Object, que em português significa Objeto de Transferência de Dados. É uma classe que tem como objetivo transportar dados entre diferentes camadas de uma aplicação, por exemplo, do banco de dados para a camada de apresentação.

Para entender melhor, podemos imaginar uma loja virtual que precisa mostrar informações de um produto para o usuário. Essas informações podem estar armazenadas no banco de dados em uma tabela "produtos". Porém, quando o usuário acessa a página de detalhes do produto, essas informações precisam ser exibidas em um formato legível e organizado.

É aí que entra o DTO. Ele é responsável por transportar as informações do produto do banco de dados para a camada de apresentação, fazendo a organização e adaptação necessárias para que as informações sejam exibidas de forma adequada.

Um DTO pode conter apenas os atributos necessários para a transferência dos dados, sem incluir métodos ou comportamentos complexos. Ele é uma classe simples, que tem como objetiv
o facilitar a comunicação entre as camadas de uma aplicação.</p>

<br>

### **Outro exemplo**
<p>Imagine que você tem um monte de objetos diferentes, cada um com suas próprias informações, como nome, idade, e-mail e telefone. Agora imagine que você precisa enviar essas informações para outro sistema, talvez até mesmo em outro formato.

Mas se você simplesmente enviasse todos esses objetos com suas informações, a outra parte teria que entender e manipular cada um individualmente. Isso pode ser complicado e demorado.

É aí que entra o DTO (Data Transfer Object). Ele é um objeto que agrupa essas informações e as organiza de uma maneira mais simples e fácil de entender. Em vez de enviar todos os objetos, você pode enviar um único DTO que contém todos os dados necessários.

O DTO é muito útil em situações em que você precisa transferir dados entre diferentes partes do sistema ou mesmo entre diferentes sistemas. Ele pode ajudar a simplificar o processo de transferência de dados e tornar as coisas mais fáceis para todos os envolvidos.</p>

<br>

---

## **RESOURCE**

<p>Em Laravel, Resource é uma classe que permite transformar dados de uma forma estruturada para serem enviados como resposta de uma API. O objetivo principal do Resource é padronizar a saída da API, para que os consumidores da API possam prever o formato da resposta e manipulá-lo de maneira adequada.

O Resource define uma estrutura para os dados, permitindo que apenas as informações necessárias sejam retornadas. Ele também fornece a possibilidade de adicionar metadados aos dados, como links ou informações adicionais, para que os consumidores da API possam usá-los em suas aplicações.

O Resource é criado como uma classe, que herda de JsonResource ou outras classes fornecidas pelo Laravel, e deve ser instanciado passando o modelo ou dados que serão transformados. A classe define o método toArray, que transforma os dados e retorna um array com os campos e valores a serem retornados.</p>

<br>

---
## **DIFERENÇA ENTRE INSTANCIAR UMA CLASSE E ACESSAR ELA User() e User::**

<p>new TrainerDTO() é usado para criar uma nova instância do objeto TrainerDTO, enquanto TrainerDTO:: é usado para chamar um método ou propriedade estática da classe TrainerDTO.

Quando usamos new TrainerDTO(), estamos criando uma nova instância do objeto TrainerDTO que pode ser usada para armazenar dados específicos de um treinador. Podemos definir os valores dos atributos da instância criada, passando os valores para o construtor da classe.

Por outro lado, quando usamos TrainerDTO::, estamos acessando um método ou propriedade estática da classe TrainerDTO. Esses métodos e propriedades estão disponíveis sem que seja necessário criar uma instância da classe. Isso pode ser útil quando queremos chamar um método ou acessar uma propriedade que não depende de uma instância específica do objeto TrainerDTO.</p>

---

<br>

# Relações Polimórficas

Configuração dos modelos:

Modelo Post:
````php
<?php

namespace App\Models;

use Illuminate\Database\Eloquent\Model;

class Post extends Model
{
    public function comments()
    {
        return $this->morphMany(Comment::class, 'commentable');
    }
}
````
Modelo Comment:

````php
<?php

namespace App\Models;

use Illuminate\Database\Eloquent\Model;

class Comment extends Model
{
    public function commentable()
    {
        return $this->morphTo();
    }
}
````
Modelo Image:

````php
<?php

namespace App\Models;

use Illuminate\Database\Eloquent\Model;

class Image extends Model
{
    public function comments()
    {
        return $this->morphMany(Comment::class, 'commentable');
    }
}
````
Migrações:
Certifique-se de que você tenha as migrações para criar as tabelas relacionadas ao Post, Comment e Image. A tabela comments deve ter os campos commentable_id, commentable_type, e outros campos necessários para os comentários.

Uso das relações:
Agora você pode utilizar as relações polimórficas em seus controladores ou em outras partes do seu código.

Exemplo de criação de um novo comentário para um post:

````php
$post = Post::find(1);
$comment = new Comment();
$comment->content = 'Novo comentário para o post';
$post->comments()->save($comment);
````

Exemplo de criação de um novo comentário para uma imagem:

````php
$image = Image::find(1);
$comment = new Comment();
$comment->content = 'Novo comentário para a imagem';
$image->comments()->save($comment);
````

Exemplo de obtenção dos comentários de um post:

````php
$post = Post::find(1);
$comments = $post->comments;
````
Exemplo de obtenção dos comentários de uma imagem:

````php
$image = Image::find(1);
$comments = $image->comments;
````
Dessa forma, você pode criar relações polimórficas no Laravel, permitindo que um modelo possa ter comentários de diferentes tipos de entidades.

<br>

##  função morphMany 

<p>
A função morphMany é uma função do Laravel que permite estabelecer uma relação "um para muitos" polimórfica entre dois modelos. Isso significa que um modelo pode ter várias instâncias de outro modelo associado a ele, mas essas instâncias podem pertencer a diferentes tipos de modelos.

Por exemplo, vamos considerar os modelos User e Comment. Cada usuário pode ter vários comentários, mas esses comentários podem ser feitos em diferentes tipos de entidades, como Post, Image, etc.

Ao usar a função morphMany, você está dizendo que um modelo pode ter várias instâncias de outro modelo associado a ele, identificando o tipo de entidade por meio de uma coluna chamada commentable_type e o ID da entidade relacionada por meio de uma coluna chamada commentable_id.

Simplificando, a função morphMany permite definir uma relação "um para muitos" polimórfica, onde um modelo pode ter vários outros modelos associados a ele, mas esses modelos podem pertencer a diferentes tipos de entidades.
</p>

## Exemplos 

Exemplo de morphMany:
Suponha que temos três modelos: User, Post e Comment, onde tanto um usuário quanto um post podem ter vários comentários. Veja como ficaria a implementação:

Migration para a tabela de comentários (comments):
````php
Schema::create('comments', function (Blueprint $table) {
    $table->id();
    $table->text('content');
    $table->unsignedBigInteger('commentable_id');
    $table->string('commentable_type');
    $table->timestamps();
});
````

Modelo User:
````php
class User extends Model
{
    public function comments()
    {
        return $this->morphMany(Comment::class, 'commentable');
    }
}
````

Modelo Post:
````php
class Post extends Model
{
    public function comments()
    {
        return $this->morphMany(Comment::class, 'commentable');
    }
}
````

Utilizando a relação morphMany:
````php
$user = User::find(1);
$comments = $user->comments;

$post = Post::find(1);
$comments = $post->comments;
````

Nesse exemplo, ao acessar a relação $user->comments ou $post->comments, obteremos todos os comentários associados ao usuário ou ao post, respectivamente. A diferença está no fato de que a coluna commentable_type será preenchida com o tipo do modelo relacionado (User ou Post) e a coluna commentable_id será preenchida com o ID correspondente.

Esses são apenas exemplos básicos para ilustrar o uso das relações hasMany e morphMany no Laravel. A implementação real pode variar dependendo das necessidades do seu projeto.