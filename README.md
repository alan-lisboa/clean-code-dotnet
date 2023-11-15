# Conceitos de Clean Code (Código Limpo) adaptado para .NET/.NET Core

Se você gostou do projeto `clean-code-dotnet` ou se ele te ajudou de alguma maneira, considere dar uma estrela :star: para este repositório. Isto irá não somente fortalecer nossa comunidade .NET mas também melhorar as habilidades de código limpo para os desenvolvedores .NET ao redor do mundo. Muito obrigado :+1:

Este projeto é baseado no projeto [clean-code-dotnet](https://github.com/thangchung/clean-code-dotnet) de [Thang Chung](https://github.com/thangchung) e você pode conferí-lo na integra clicando neste [link](https://github.com/thangchung/clean-code-dotnet). Você pode também ter mais informações no [blog](https://medium.com/@thangchung) do autor ou mandando um `Oi` para ele no [Twitter](https://twitter.com/thangchung)!

# Conteúdo

- [Conceitos de Clean Code (Código Limpo) adaptado para .NET/.NET Core](#conceitos-de-clean-code-código-limpo-adaptado-para-netnet-core)
- [Conteúdo](#conteúdo)
- [Introdução](#introdução)
- [Clean Code .NET](#clean-code-net)
  - [Nomeação (Naming)](#nomeação-naming)
  - [Variáveis](#variáveis)
  - [Funções](#funções)
  - [Objetos e estruturas de dados](#objetos-e-estruturas-de-dados)
  - [Classes](#classes)
  - [SOLID](#solid)
  - [Testes](#testes)
  - [Concorrência](#concorrência)
  - [Tratamento de Erros (Error Handling)](#tratamento-de-erros-error-handling)
  - [Formatação](#formatação)
  - [Comentários](#comentários)
- [Outros Recursos de Clean Code](#outros-recursos-de-clean-code)
  - [Outras listas de Clean Code](#outras-listas-de-clean-code)
  - [Guia de Estilos](#guia-de-estilos)
  - [Ferramentas](#ferramentas)
  - [Cheatsheets](#cheatsheets)

# Introdução

![Imagem engraçada da estimativa, pela qualidade de software, de quantos palavrões você grita ao ler o código](http://www.osnews.com/images/comics/wtfm.jpg)

Software engineering principles, livro de Robert C. Martin's [_Clean Code_](https://www.amazon.com/Clean-Code-Handbook-Software-Craftsmanship/dp/0132350882), adaptado para .NET/.NET Core. Este documento não é um guia de estilos. Este documento é um guia de como produzir software com código legível, reusável e refatorável em .NET/.NET Core.

Nem todos os princípios aqui contidos devem ser rigorosamente seguidos, e muito menos estão universalmente acordados. Aqui você encontrará somente algumas diretrizes e nada mais, que foram codificadas ao longo de muitos anos de experiência coletiva pelos autores do _Clean Code_.

Inspirado nas listas [clean-code-javascript](https://github.com/ryanmcdermott/clean-code-javascript) e [clean-code-php](https://github.com/jupeter/clean-code-php).

# Clean Code .NET

## Nomeação (Naming)

<details>
  <summary><b>Evite usar nomes ruins</b></summary>
<br />

Um bom nome permite que o código possa ser utilizado por muitos desenvolvedores. O nome deve refletir o que faz e dar o contexto.
<br />

:x: **Errado**

```csharp
int d;
```

:heavy_check_mark: **Correto**

```csharp
int diasAposModificacao;
```

**[⬆ Voltar ao topo](#conteúdo)**

</details>

<details>
  <summary><b>Evite nomes enganosos</b></summary>
<br />

Nomeie a variável para refletir para que ela é usada.
<br />

:x: **Errado**

```csharp
var dadosBanco = db.ObterDados().ToList();
```

:heavy_check_mark: **Correto**

```csharp
var listaColaboradores = _colaboradorService.ObterColaboradores().ToList();
```

**[⬆ Voltar ao topo](#conteúdo)**

</details>

<details>
  <summary><b>Evite a notação húngara</b></summary>
<br />

A notação húngara reafirma o tipo que já está presente na declaração. Isso é inútil, pois os IDEs modernos já fazem isso.
<br />

:x: **Errado**

```csharp
int iContador;
string strNomeCompleto;
DateTime dDataModificacao;
```

:heavy_check_mark: **Correto**

```csharp
int contador;
string nomeCompleto;
DateTime dataModificacao;
```

A notação húngara também não deve ser usada em parâmetros.

:x: **Errado**

```csharp
public bool VerificarLojaAberta(string pDia, int pTotal)
{
    // alguma lógica
}
```

:heavy_check_mark: **Correto**

```csharp
public bool VerificarLojaAberta(string dia, int total)
{
    // alguma lógica
}
```

**[⬆ Voltar ao topo](#conteúdo)**

</details>

<details>
  <summary><b>Use uma capitalização consistente</b></summary>
<br />

A capitalização diz muito sobre suas variáveis, funções, etc. 
Essas regras são subjetivas, porém sua equipe pode escolher como eles querem utilizar.<br />
A questão é: não importa o que vocês escolham, apenas sejam consistentes.
<br />

:x: **Errado**

```csharp
const int DIAS_NA_SEMANA = 7;
const int diasNoMes = 30;

var musicas = new List<string> { 'Back In Black', 'Stairway to Heaven', 'Hey Jude' };
var Artistas = new List<string> { 'ACDC', 'Led Zeppelin', 'The Beatles' };

bool ApagarBancoDeDados() {}
bool Restaurar_BancoDeDados() {}

class animal {}
class Alpaca {}
```

:heavy_check_mark: **Correto**

```csharp
const int DiasNaSemana = 7;
const int DiasNoMes = 30;

var musicas = new List<string> { 'Back In Black', 'Stairway to Heaven', 'Hey Jude' };
var artistas = new List<string> { 'ACDC', 'Led Zeppelin', 'The Beatles' };

bool ApagarBancoDeDados() {}
bool RestaurarBancoDeDados() {}

class Animal {}
class Alpaca {}
```

**[⬆ Voltar ao topo](#conteúdo)**

</details>

<details>
  <summary><b>Use nomes pronunciáveis</b></summary>
<br />

Levará um bom tempo para investigar o significado das variáveis e funções quando elas não puderem ser pronunciadas.
<br />

:x: **Errado**

```csharp
public class Colaborador
{
    public Datetime dtinitrab { get; set; } // Que diabos é isso
    public Datetime hrmod { get; set; } // Mesma coisa
}
```

:heavy_check_mark: **Correto**

```csharp
public class Employee
{
    public Datetime DataInicioTrabalho { get; set; }
    public Datetime HoraModificacao { get; set; }
}
```

**[⬆ Voltar ao topo](#conteúdo)**

</details>

<details>
  <summary><b>Use a notação camelCase</b></summary>
<br />

Use [Notação Camelcase](https://en.wikipedia.org/wiki/Camel_case) para variáveis e parâmetros no método.
<br />

:x: **Errado**

```csharp
var telefonecolaborador;

public double CalcularSalario(int diastrabalhados, int horastrabalhadas)
{
    // alguma lógica
}
```

:heavy_check_mark: **Correto**

```csharp
var telefoneColaborador;

public double CalcularSalario(int diasTrabalhados, int horasTrabalhadas)
{
    // alguma lógica
}
```

**[⬆ Voltar ao topo](#conteúdo)**

</details>

<details>
  <summary><b>Use nomes que identificam o domínio</b></summary>
<br />

As pessoas que leem seu código também são programadores. Nomear as coisas corretamente ajudará todos a estarem na mesma página.<br />
Não queremos perder tempo explicando a todos para que serve uma variável ou função.
<br />

:heavy_check_mark: **Correto**

```csharp
public class SingleObject
{
    // create an object of SingleObject
    private static SingleObject _instance = new SingleObject();

    // make the constructor private so that this class cannot be instantiated
    private SingleObject() {}

    // get the only object available
    public static SingleObject GetInstance()
    {
        return _instance;
    }

    public string ShowMessage()
    {
        return "Hello World!";
    }
}

public static void main(String[] args)
{
    // illegal construct
    // var object = new SingleObject();

    // Get the only object available
    var singletonObject = SingleObject.GetInstance();

    // show the message
    singletonObject.ShowMessage();
}
```

**[⬆ Voltar ao topo](#conteúdo)**

</details>

## Variáveis

<details>
  <summary><b>Evite aninhar profundamente blocos condicionais, e retorne antes sempre que puder</b></summary>
<br />

Muitas instruções _if/else_ podem dificultar o acompanhamento do código. **Explícito é melhor que implícito**
<br />

:x: **Errado**

```csharp
public bool IsShopOpen(string day)
{
    if (!string.IsNullOrEmpty(day))
    {
        day = day.ToLower();
        if (day == "friday")
        {
            return true;
        }
        else if (day == "saturday")
        {
            return true;
        }
        else if (day == "sunday")
        {
            return true;
        }
        else
        {
            return false;
        }
    }
    else
    {
        return false;
    }

}
```

:heavy_check_mark: **Correto**

```csharp
public bool IsShopOpen(string day)
{
    if (string.IsNullOrEmpty(day))
    {
        return false;
    }

    var openingDays = new[] { "friday", "saturday", "sunday" };
    return openingDays.Any(d => d == day.ToLower());
}
```

:x: **Errado**

```csharp
public long Fibonacci(int n)
{
    if (n < 50)
    {
        if (n != 0)
        {
            if (n != 1)
            {
                return Fibonacci(n - 1) + Fibonacci(n - 2);
            }
            else
            {
                return 1;
            }
        }
        else
        {
            return 0;
        }
    }
    else
    {
        throw new System.Exception("Not supported");
    }
}
```

:heavy_check_mark: **Correto**

```csharp
public long Fibonacci(int n)
{
    if (n == 0)
    {
        return 0;
    }

    if (n == 1)
    {
        return 1;
    }

    if (n > 50)
    {
        throw new System.Exception("Not supported");
    }

    return Fibonacci(n - 1) + Fibonacci(n - 2);
}
```

**[⬆ Voltar ao topo](#conteúdo)**

</details>

<details>
  <summary><b>Evite o mapeamento mental</b></summary>
<br />

Não force o leitor do seu código a traduzir o que a variável significa. **Explícito é melhor que implícito**.
<br />

:x: **Errado**

```csharp
var l = new[] { "Austin", "New York", "San Francisco" };

for (var i = 0; i < l.Count(); i++)
{
    var li = l[i];
    DoStuff();
    DoSomeOtherStuff();

    // ...
    // ...
    // ...
    // Wait, what is `li` for again?
    Dispatch(li);
}
```

:heavy_check_mark: **Correto**

```csharp
var locations = new[] { "Austin", "New York", "San Francisco" };

foreach (var location in locations)
{
    DoStuff();
    DoSomeOtherStuff();

    // ...
    // ...
    // ...
    Dispatch(location);
}
```

**[⬆ Voltar ao topo](#conteúdo)**

</details>

<details>
  <summary><b>Evite a string mágica</b></summary>
<br />

Strings mágicas são valores de string especificados diretamente no código do aplicativo que têm impacto no comportamento do aplicativo.<br />
Freqüentemente, essas strings acabarão sendo duplicadas dentro do sistema e, como não podem ser atualizadas automaticamente usando ferramentas de refatoração, elas se tornam uma fonte comum de bugs quando alterações são feitas em algumas strings, mas não em outras.
<br />

:x: **Errado**

```csharp
if (userRole == "Admin")
{
    // logic in here
}
```

:heavy_check_mark: **Correto**

```csharp
const string ADMIN_ROLE = "Admin";

if (userRole == ADMIN_ROLE)
{
    // logic in here
}
```
Usando desta forma, teremos só que mudar no local centralizado e todos os outros pontos do sistema irão adaptar-se.

**[⬆ Voltar ao topo](#conteúdo)**

</details>

<details>
  <summary><b>Não adicione contexto desnecessário</b></summary>
<br />

Se o nome da sua classe/objeto lhe disser algo, não repita isso no nome da sua variável.
<br />

:x: **Errado**

```csharp
public class Car
{
    public string CarMake { get; set; }
    public string CarModel { get; set; }
    public string CarColor { get; set; }

    //...
}
```

:heavy_check_mark: **Correto**

```csharp
public class Car
{
    public string Make { get; set; }
    public string Model { get; set; }
    public string Color { get; set; }

    //...
}
```

**[⬆ Voltar ao topo](#conteúdo)**

</details>

<details>
  <summary><b>Use nomes significativos e pronunciáveis para as variáveis</b></summary>
<br />

:x: **Errado**

```csharp
var ymdstr = DateTime.UtcNow.ToString("MMMM dd, yyyy");
```

:heavy_check_mark: **Correto**

```csharp
var currentDate = DateTime.UtcNow.ToString("MMMM dd, yyyy");
```

**[⬆ Voltar ao topo](#conteúdo)**

</details>

<details>
  <summary><b>Use o mesmo vocabulário para o mesmo tipo de variável</b></summary>
<br />

:x: **Errado**

```csharp
GetUserInfo();
GetUserData();
GetUserRecord();
GetUserProfile();
```

:heavy_check_mark: **Correto**

```csharp
GetUser();
```

**[⬆ Voltar ao topo](#conteúdo)**

</details>

<details>
  <summary><b>Use nomes pesquisáveis (parte 1)</b></summary>
<br />

Leremos mais código do que escreveremos. É importante que o código que escrevemos seja legível e pesquisável.<br />
Ao _não_ nomear variáveis que acabam sendo significativas para a compreensão do nosso programa, prejudicamos nossos leitores.<br />
**Torne seus nomes pesquisáveis.**
<br />

:x: **Errado**

```csharp
// Para que serve o 'data'?
var data = new { Name = "John", Age = 42 };

var stream1 = new MemoryStream();
var ser1 = new DataContractJsonSerializer(typeof(object));
ser1.WriteObject(stream1, data);

stream1.Position = 0;
var sr1 = new StreamReader(stream1);
Console.Write("JSON form of Data object: ");
Console.WriteLine(sr1.ReadToEnd());
```

:heavy_check_mark: **Correto**

```csharp
var person = new Person
{
    Name = "John",
    Age = 42
};

var stream2 = new MemoryStream();
var ser2 = new DataContractJsonSerializer(typeof(Person));
ser2.WriteObject(stream2, person);

stream2.Position = 0;
var sr2 = new StreamReader(stream2);
Console.Write("JSON form of Data object: ");
Console.WriteLine(sr2.ReadToEnd());
```

**[⬆ Voltar ao topo](#conteúdo)**

</details>

<details>
  <summary><b>Use nomes pesquisáveis (parte 2)</b></summary>
 <br />

:x: **Errado**

```csharp
var data = new { Name = "John", Age = 42, PersonAccess = 4};

// Para que serve o 4?
if (data.PersonAccess == 4)
{
    // editar ...
}
```

:heavy_check_mark: **Correto**

```csharp
public enum PersonAccess : int
{
    ACCESS_READ = 1,
    ACCESS_CREATE = 2,
    ACCESS_UPDATE = 4,
    ACCESS_DELETE = 8
}

var person = new Person
{
    Name = "John",
    Age = 42,
    PersonAccess= PersonAccess.ACCESS_CREATE
};

if (person.PersonAccess == PersonAccess.ACCESS_UPDATE)
{
    // editar ...
}
```

**[⬆ Voltar ao topo](#conteúdo)**

</details>

<details>
  <summary><b>Use variáveis explicativas</b></summary>
<br />

:x: **Errado**

```csharp
const string Address = "One Infinite Loop, Cupertino 95014";
var cityZipCodeRegex = @"/^[^,\]+[,\\s]+(.+?)\s*(\d{5})?$/";
var matches = Regex.Matches(Address, cityZipCodeRegex);
if (matches[0].Success == true && matches[1].Success == true)
{
    SaveCityZipCode(matches[0].Value, matches[1].Value);
}
```

:heavy_check_mark: **Correto**

Diminua a dependência de regex nomeando subpadrões.

```csharp
const string Address = "One Infinite Loop, Cupertino 95014";
var cityZipCodeWithGroupRegex = @"/^[^,\]+[,\\s]+(?<city>.+?)\s*(?<zipCode>\d{5})?$/";
var matchesWithGroup = Regex.Match(Address, cityZipCodeWithGroupRegex);
var cityGroup = matchesWithGroup.Groups["city"];
var zipCodeGroup = matchesWithGroup.Groups["zipCode"];
if(cityGroup.Success == true && zipCodeGroup.Success == true)
{
    SaveCityZipCode(cityGroup.Value, zipCodeGroup.Value);
}
```

**[⬆ Voltar ao topo](#conteúdo)**

</details>

<details>
  <summary><b>Use argumentos padrão em vez de curto-circuito ou condicionais</b></summary>
<br />

:x: **Errado**

Isso não é bom porque `breweryName` pode ser de fato `NULL`.

```csharp
public void CreateMicrobrewery(string name = null)
{
    var breweryName = !string.IsNullOrEmpty(name) ? name : "Hipster Brew Co.";
    // ...
}
```

:heavy_check_mark: **Correto**

```csharp
public void CreateMicrobrewery(string breweryName = "Hipster Brew Co.")
{
    // ...
}
```

**[⬆ Voltar ao topo](#conteúdo)**

</details>

## Funções

<details>
  <summary><b>Evite efeitos colaterais</b></summary>
<br />

Uma função produz um efeito colateral se fizer qualquer coisa além de receber um valor e retornar outro valor ou valores. Um efeito colateral pode ser gravar em um arquivo, modificar alguma variável global ou transferir acidentalmente todo o seu dinheiro para um estranho.

Agora, você precisa ter efeitos colaterais em um programa ocasionalmente. Como no exemplo anterior, pode ser necessário gravar em um arquivo. O que você quer fazer é centralizar onde você está fazendo isso. Não tenha várias funções e classes que gravem em um arquivo específico. Tenha um serviço que faça isso. Um e somente um.

O ponto principal é evitar armadilhas comuns, como compartilhar estado entre objetos sem qualquer estrutura, usar tipos de dados mutáveis que podem ser gravados por qualquer coisa e não centralizar onde ocorrem os efeitos colaterais. Se você puder fazer isso, você será mais feliz do que a grande maioria dos outros programadores.
<br />

:x: **Errado**

```csharp
// Global variable referenced by following function.
// If we had another function that used this name, now it'd be an array and it could break it.
var name = "Ryan McDermott";

public void SplitAndEnrichFullName()
{
    var temp = name.Split(" ");
    name = $"His first name is {temp[0]}, and his last name is {temp[1]}"; // side effect
}

SplitAndEnrichFullName();

Console.WriteLine(name); // His first name is Ryan, and his last name is McDermott
```

:heavy_check_mark: **Correto**

```csharp
public string SplitAndEnrichFullName(string name)
{
    var temp = name.Split(" ");
    return $"His first name is {temp[0]}, and his last name is {temp[1]}";
}

var name = "Ryan McDermott";
var fullName = SplitAndEnrichFullName(name);

Console.WriteLine(name); // Ryan McDermott
Console.WriteLine(fullName); // His first name is Ryan, and his last name is McDermott
```

**[⬆ Voltar ao topo](#conteúdo)**

</details>

<details>
  <summary><b>Evite condicionais negativas</b></summary>
<br />

:x: **Errado**

```csharp
public bool IsDOMNodeNotPresent(string node)
{
    // ...
}

if (!IsDOMNodeNotPresent(node))
{
    // ...
}
```

:heavy_check_mark: **Correto**

```csharp
public bool IsDOMNodePresent(string node)
{
    // ...
}

if (IsDOMNodePresent(node))
{
    // ...
}
```

**[⬆ Voltar ao topo](#conteúdo)**

</details>

<details>
  <summary><b>Evite condicionais usando polimorfismo</b></summary>
<br />

Esta parece ser uma tarefa impossível. Ao ouvir isso pela primeira vez, a maioria das pessoas diz: "como posso fazer algo sem uma declaração `if`?". <br />
A resposta é que você pode usar o polimorfismo para realizar a mesma tarefa em muitos casos.<br />

A segunda pergunta geralmente é: "bem, isso é ótimo, mas por que eu iria querer fazer isso?"<br />
A resposta é um conceito anterior de código limpo que aprendemos: uma função só deve fazer uma Coisa. Quando você tem classes e funções que possuem instruções `if`, você está dizendo ao usuário que sua função faz mais de uma coisa.<br />

**Lembre-se, faça apenas uma coisa.**
<br />

:x: **Errado**

```csharp
class Airplane
{
    // ...

    public double GetCruisingAltitude()
    {
        switch (_type)
        {
            case '777':
                return GetMaxAltitude() - GetPassengerCount();
            case 'Air Force One':
                return GetMaxAltitude();
            case 'Cessna':
                return GetMaxAltitude() - GetFuelExpenditure();
        }
    }
}
```

:heavy_check_mark: **Correto**

```csharp
interface IAirplane
{
    // ...

    double GetCruisingAltitude();
}

class Boeing777 : IAirplane
{
    // ...

    public double GetCruisingAltitude()
    {
        return GetMaxAltitude() - GetPassengerCount();
    }
}

class AirForceOne : IAirplane
{
    // ...

    public double GetCruisingAltitude()
    {
        return GetMaxAltitude();
    }
}

class Cessna : IAirplane
{
    // ...

    public double GetCruisingAltitude()
    {
        return GetMaxAltitude() - GetFuelExpenditure();
    }
}
```

**[⬆ Voltar ao topo](#conteúdo)**

</details>

<details>
  <summary><b>Evite a verificação de tipos (parte 1)</b></summary>
<br />

:x: **Errado**

```csharp
public Path TravelToTexas(object vehicle)
{
    if (vehicle.GetType() == typeof(Bicycle))
    {
        (vehicle as Bicycle).PeddleTo(new Location("texas"));
    }
    else if (vehicle.GetType() == typeof(Car))
    {
        (vehicle as Car).DriveTo(new Location("texas"));
    }
}
```

:heavy_check_mark: **Correto**

```csharp
public Path TravelToTexas(Traveler vehicle)
{
    vehicle.TravelTo(new Location("texas"));
}
```

:heavy_check_mark: **Correto**

```csharp
// pattern matching
public Path TravelToTexas(object vehicle)
{
    if (vehicle is Bicycle bicycle)
    {
        bicycle.PeddleTo(new Location("texas"));
    }
    else if (vehicle is Car car)
    {
        car.DriveTo(new Location("texas"));
    }
}
```

**[⬆ Voltar ao topo](#conteúdo)**

</details>

<details>
  <summary><b>Evite a verificação de tipos (parte 2)</b></summary>
<br />

:x: **Errado**

```csharp
public int Combine(dynamic val1, dynamic val2)
{
    int value;
    if (!int.TryParse(val1, out value) || !int.TryParse(val2, out value))
    {
        throw new Exception('Must be of type Number');
    }

    return val1 + val2;
}
```

:heavy_check_mark: **Correto**

```csharp
public int Combine(int val1, int val2)
{
    return val1 + val2;
}
```

**[⬆ Voltar ao topo](#conteúdo)**

</details>

<details>
  <summary><b>Evite flags nos parâmetros do método</b></summary>
<br />

Uma `flag` indica que o método tem mais de uma responsabilidade. É melhor que o método tenha apenas uma única responsabilidade.<br />
Divida o método em dois se um parâmetro booleano adicionar múltiplas responsabilidades ao método.
<br />

:x: **Errado**

```csharp
public void CreateFile(string name, bool temp = false)
{
    if (temp)
    {
        Touch("./temp/" + name);
    }
    else
    {
        Touch(name);
    }
}
```

:heavy_check_mark: **Correto**

```csharp
public void CreateFile(string name)
{
    Touch(name);
}

public void CreateTempFile(string name)
{
    Touch("./temp/"  + name);
}
```

**[⬆ Voltar ao topo](#conteúdo)**

</details>

<details>
  <summary><b>Não escreva em funções globais</b></summary>
<br />

Poluir globais é uma prática ruim em muitas linguagens porque você poderia entrar em conflito com outra biblioteca e o usuário de sua API não saberia até obter uma exceção na produção. Vamos pensar em um exemplo: e se você quisesse ter um array de configuração.<br />

Você poderia escrever uma função global como `Config()`, mas ela poderia entrar em conflito com outra biblioteca que tentasse fazer a mesma coisa.
<br />

:x: **Errado**

```csharp
public Dictionary<string, string> Config()
{
    return new Dictionary<string,string>(){
        ["foo"] = "bar"
    };
}
```

:heavy_check_mark: **Correto**

```csharp
class Configuration
{
    private Dictionary<string, string> _configuration;

    public Configuration(Dictionary<string, string> configuration)
    {
        _configuration = configuration;
    }

    public string Get(string key)
    {
        return _configuration.ContainsKey(key) ? _configuration[key] : null;
    }
}
```

Carregar configuração e criar instância da classe `Configuration`

```csharp
var configuration = new Configuration(new Dictionary<string, string>() {
    ["foo"] = "bar"
});
```
E agora você deve usar a instância de `Configuração` em sua aplicação.

```csharp
var fooValue = configuration.Get("foo");
```

**[⬆ Voltar ao topo](#conteúdo)**

</details>

<details>
  <summary><b>Não use o padrão Singleton</b></summary>
<br />

Singleton é um [anti-pattern](https://en.wikipedia.org/wiki/Singleton_pattern) e não deve ser usado. Parafraseado por Brian Button:

1. Eles geralmente são usados como uma **instância global** e por que isso é tão ruim? Porque **você oculta as dependências** da sua aplicação no seu código, em vez de expô-las através das interfaces. Tornar algo global para evitar distribuí-lo é um [Code Smell](https://en.wikipedia.org/wiki/Code_smell).
2. Eles violam o [princípio de responsabilidade única](#single-responsibility-principle-srp): em virtude do fato de que **eles controlam sua própria criação e ciclo de vida**.
3. Eles inerentemente fazem com que o código seja fortemente [acoplado](https://en.wikipedia.org/wiki/Coupling_%28computer_programming%29). Isso torna bastante difícil falsea-los durante os **testes** na maioria dos casos.
4. Eles carregam o estado durante toda a vida útil da aplicação. Isso pode ocasionar problemas nos testes unitários porque um teste pode considerar o estado do objeto resultante de outro teste anterior, e ocasionar um resultado de falso/positivo. Cada teste unitário deve ser independente um do outro.

Também há considerações muito boas de [Misko Hevery](http://misko.hevery.com/about/) sobre a [raiz do problema](http://misko.hevery.com/2008/08/25/root-cause-of-singletons/).
<br />

:x: **Errado**

```csharp
class DBConnection
{
    private static DBConnection _instance;

    private DBConnection()
    {
        // ...
    }

    public static GetInstance()
    {
        if (_instance == null)
        {
            _instance = new DBConnection();
        }

        return _instance;
    }

    // ...
}

var singleton = DBConnection.GetInstance();
```

:heavy_check_mark: **Correto**

```csharp
class DBConnection
{
    public DBConnection(IOptions<DbConnectionOption> options)
    {
        // ...
    }

    // ...
}
```

Crie uma instância da classe `DBConnection` e configure-a com o [Option pattern](https://docs.microsoft.com/en-us/aspnet/core/fundamentals/configuration/options?view=aspnetcore-2.1).

```csharp
var options = <resolve from IOC>;
var connection = new DBConnection(options);
```

E agora você pode usar a instância de `DBConnection` em sua aplicação.

**[⬆ Voltar ao topo](#conteúdo)**

</details>

<details>
  <summary><b>Argumentos de função (2 ou menos, idealmente)</b></summary>
<br />

Limitar a quantidade de parâmetros de função é extremamente importante porque facilita o teste de sua função. Ter mais de três leva a uma explosão combinatória onde você terá que testar vários casos diferentes com cada argumento separado.

Zero argumentos é o caso ideal. Um ou dois argumentos são aceitáveis e três devem ser evitados. Qualquer coisa além disso deve ser consolidada. Normalmente, se você tiver mais de dois argumentos, sua função está tentando fazer muita coisa. Nos casos em que não é, na maioria das vezes um objeto de nível superior será suficiente como argumento.

​
:x: **Errado**

```csharp
public void CreateMenu(string title, string body, string buttonText, bool cancellable)
{
    // ...
}
```

:heavy_check_mark: **Correto**

```csharp
public class MenuConfig
{
    public string Title { get; set; }
    public string Body { get; set; }
    public string ButtonText { get; set; }
    public bool Cancellable { get; set; }
}

var config = new MenuConfig
{
    Title = "Foo",
    Body = "Bar",
    ButtonText = "Baz",
    Cancellable = true
};

public void CreateMenu(MenuConfig config)
{
    // ...
}
```

**[⬆ Voltar ao topo](#conteúdo)**

</details>

<details>
  <summary><b>Funções devem fazer somente uma coisa</b></summary>
<br />

Esta é de longe a regra mais importante na engenharia de software. <br />

Quando as funções fazem mais de uma coisa, são mais difíceis de compor, testar e raciocinar. Quando você pode isolar uma função para apenas uma ação, elas podem ser refatoradas facilmente e seu código será lido com mais facilidade.<br />

Se você não tirar nada deste guia além deste tópico, estará à frente de muitos desenvolvedores.
<br />

:x: **Errado**

```csharp
public void SendEmailToListOfClients(string[] clients)
{
    foreach (var client in clients)
    {
        var clientRecord = db.Find(client);
        if (clientRecord.IsActive())
        {
            Email(client);
        }
    }
}
```

:heavy_check_mark: **Correto**

```csharp
public void SendEmailToListOfClients(string[] clients)
{
    var activeClients = GetActiveClients(clients);
    // Do some logic
}

public List<Client> GetActiveClients(string[] clients)
{
    return db.Find(clients).Where(s => s.Status == "Active");
}
```

**[⬆ Voltar ao topo](#conteúdo)**

</details>

<details>
  <summary><b>Os nomes das funções devem dizer o que fazem</b></summary>
<br />

:x: **Errado**

```csharp
public class Email
{
    //...

    public void Handle()
    {
        SendMail(this._to, this._subject, this._body);
    }
}

var message = new Email(...);
// O que é isto? Um manipulador para a mensagem? Nós estamos escrevendo para um arquivo agora?
message.Handle();
```

:heavy_check_mark: **Correto**

```csharp
public class Email
{
    //...

    public void Send()
    {
        SendMail(this._to, this._subject, this._body);
    }
}

var message = new Email(...);
// Claro e óbvio
message.Send();
```

**[⬆ Voltar ao topo](#conteúdo)**

</details>

<details>
  <summary><b>As funções devem ter apenas um nível de abstração</b></summary>
<br />

> Carece de mais explicação

Quando você tem mais de um nível de abstração, sua função geralmente está fazendo muita coisa. A divisão de funções leva à reutilização e a testes mais fáceis.
<br />

:x: **Errado**

```csharp
public string ParseBetterJSAlternative(string code)
{
    var regexes = [
        // ...
    ];

    var statements = explode(" ", code);
    var tokens = new string[] {};
    foreach (var regex in regexes)
    {
        foreach (var statement in statements)
        {
            // ...
        }
    }

    var ast = new string[] {};
    foreach (var token in tokens)
    {
        // lex...
    }

    foreach (var node in ast)
    {
        // parse...
    }
}
```

:x: **Errado também**

Realizamos algumas funcionalidades, mas a função `ParseBetterJSAlternative()` ainda é muito complexa e não pode ser testada.

```csharp
public string Tokenize(string code)
{
    var regexes = new string[]
    {
        // ...
    };

    var statements = explode(" ", code);
    var tokens = new string[] {};
    foreach (var regex in regexes)
    {
        foreach (var statement in statements)
        {
            tokens[] = /* ... */;
        }
    }

    return tokens;
}

public string Lexer(string[] tokens)
{
    var ast = new string[] {};
    foreach (var token in tokens)
    {
        ast[] = /* ... */;
    }

    return ast;
}

public string ParseBetterJSAlternative(string code)
{
    var tokens = Tokenize(code);
    var ast = Lexer(tokens);
    foreach (var node in ast)
    {
        // parse...
    }
}
```

:heavy_check_mark: **Correto**

A melhor solução é remover as dependências da função `ParseBetterJSAlternative()`.

```csharp
class Tokenizer
{
    public string Tokenize(string code)
    {
        var regexes = new string[] {
            // ...
        };

        var statements = explode(" ", code);
        var tokens = new string[] {};
        foreach (var regex in regexes)
        {
            foreach (var statement in statements)
            {
                tokens[] = /* ... */;
            }
        }

        return tokens;
    }
}

class Lexer
{
    public string Lexify(string[] tokens)
    {
        var ast = new[] {};
        foreach (var token in tokens)
        {
            ast[] = /* ... */;
        }

        return ast;
    }
}

class BetterJSAlternative
{
    private string _tokenizer;
    private string _lexer;

    public BetterJSAlternative(Tokenizer tokenizer, Lexer lexer)
    {
        _tokenizer = tokenizer;
        _lexer = lexer;
    }

    public string Parse(string code)
    {
        var tokens = _tokenizer.Tokenize(code);
        var ast = _lexer.Lexify(tokens);
        foreach (var node in ast)
        {
            // parse...
        }
    }
}
```

**[⬆ Voltar ao topo](#conteúdo)**

</details>

<details>
  <summary><b>Chamadores e receptores de funções devem estar próximos</b></summary>
<br />

Se uma função chamar outra, mantenha essas funções fechadas verticalmente no arquivo de origem.<br />
O ideal é manter o chamador logo acima do receptor. Tendemos a ler o código de cima para baixo, como um jornal. Por causa disso, faça seu código ser lido dessa maneira.
<br />

:x: **Errado**

```csharp
class PerformanceReview
{
    private readonly Employee _employee;

    public PerformanceReview(Employee employee)
    {
        _employee = employee;
    }

    private IEnumerable<PeersData> LookupPeers()
    {
        return db.lookup(_employee, 'peers');
    }

    private ManagerData LookupManager()
    {
        return db.lookup(_employee, 'manager');
    }

    private IEnumerable<PeerReviews> GetPeerReviews()
    {
        var peers = LookupPeers();
        // ...
    }

    public PerfReviewData PerfReview()
    {
        GetPeerReviews();
        GetManagerReview();
        GetSelfReview();
    }

    public ManagerData GetManagerReview()
    {
        var manager = LookupManager();
    }

    public EmployeeData GetSelfReview()
    {
        // ...
    }
}

var  review = new PerformanceReview(employee);
review.PerfReview();
```

:heavy_check_mark: **Correto**

```csharp
class PerformanceReview
{
    private readonly Employee _employee;

    public PerformanceReview(Employee employee)
    {
        _employee = employee;
    }

    public PerfReviewData PerfReview()
    {
        GetPeerReviews();
        GetManagerReview();
        GetSelfReview();
    }

    private IEnumerable<PeerReviews> GetPeerReviews()
    {
        var peers = LookupPeers();
        // ...
    }

    private IEnumerable<PeersData> LookupPeers()
    {
        return db.lookup(_employee, 'peers');
    }

    private ManagerData GetManagerReview()
    {
        var manager = LookupManager();
        return manager;
    }

    private ManagerData LookupManager()
    {
        return db.lookup(_employee, 'manager');
    }

    private EmployeeData GetSelfReview()
    {
        // ...
    }
}

var review = new PerformanceReview(employee);
review.PerfReview();
```

**[⬆ Voltar ao topo](#conteúdo)**

</details>

<details>
  <summary><b>Encapsule condicionais</b></summary>
<br />

:x: **Errado**

```csharp
if (article.state == "published")
{
    // ...
}
```

:heavy_check_mark: **Correto**

```csharp
if (article.IsPublished())
{
    // ...
}
```

**[⬆ Voltar ao topo](#conteúdo)**

</details>

<details>
  <summary><b>Remova o código morto</b></summary>
<br />

Código morto é tão ruim quanto código duplicado. Não há razão para mantê-lo em sua base de código.<br />
Se não estiver sendo chamado, livre-se dele! Ainda estará seguro em seu histórico de versões se você ainda precisar dele.
<br />

:x: **Errado**

```csharp
public void OldRequestModule(string url)
{
    // ...
}

public void NewRequestModule(string url)
{
    // ...
}

var request = NewRequestModule(requestUrl);
InventoryTracker("apples", request, "www.inventory-awesome.io");
```

:heavy_check_mark: **Correto**

```csharp
public void RequestModule(string url)
{
    // ...
}

var request = RequestModule(requestUrl);
InventoryTracker("apples", request, "www.inventory-awesome.io");
```

**[⬆ Voltar ao topo](#conteúdo)**

</details>

## Objetos e estruturas de dados

<details>
  <summary><b>Use getters e setters</b></summary>
<br />

Em C#/VB.NET você pode definir palavras-chave `public`, `protected` e `private` para métodos.
Usando isto, você pode controlar a modificação de propriedades em um objeto.

- Quando você quiser fazer mais além de obter uma propriedade de objeto, não precisará procurar e alterar todos os acessadores em sua base de código.
- Simplifica a adição de validação ao fazer um `set`.
- Encapsula a representação interna.
- Fácil de adicionar registro e tratamento de erros ao obter ou definir valores.
- Herdando esta classe, você pode substituir a funcionalidade padrão.
- Você pode carregar sobre demanda as propriedades do seu objeto.

Além disso, isso faz parte do princípio Aberto/Fechado, dos princípios de design orientado a objetos.
<br />

:x: **Errado**

```csharp
class BankAccount
{
    public double Balance = 1000;
}

var bankAccount = new BankAccount();

// Fake buy shoes...
bankAccount.Balance -= 100;
```

:heavy_check_mark: **Correto**

```csharp
class BankAccount
{
    private double _balance = 0.0D;

    pubic double Balance {
        get {
            return _balance;
        }
    }

    public BankAccount(balance = 1000)
    {
       _balance = balance;
    }

    public void WithdrawBalance(int amount)
    {
        if (amount > _balance)
        {
            throw new Exception('Amount greater than available balance.');
        }

        _balance -= amount;
    }

    public void DepositBalance(int amount)
    {
        _balance += amount;
    }
}

var bankAccount = new BankAccount();

// Buy shoes...
bankAccount.WithdrawBalance(price);

// Get balance
balance = bankAccount.Balance;
```

**[⬆ Voltar ao topo](#conteúdo)**

</details>

<details>
  <summary><b>Faça com que os objetos tenham membros privados/protegidos</b></summary>
<br />

:x: **Errado**

```csharp
class Employee
{
    public string Name { get; set; }

    public Employee(string name)
    {
        Name = name;
    }
}

var employee = new Employee("John Doe");
Console.WriteLine(employee.Name); // Employee name: John Doe
```

:heavy_check_mark: **Correto**

```csharp
class Employee
{
    public string Name { get; }

    public Employee(string name)
    {
        Name = name;
    }
}

var employee = new Employee("John Doe");
Console.WriteLine(employee.Name); // Employee name: John Doe
```

**[⬆ Voltar ao topo](#conteúdo)**

</details>

## Classes

<details>
  <summary><b>Use encadeamento de métodos</b></summary>
<br />

Este padrão é muito útil e comumente usado em muitas bibliotecas. Ele permite que seu código seja expressivo e menos detalhado.<br />
Por esse motivo, use o encadeamento de métodos e veja como seu código ficará limpo.
<br />

:heavy_check_mark: **Correto**

```csharp
public static class ListExtensions
{
    public static List<T> FluentAdd<T>(this List<T> list, T item)
    {
        list.Add(item);
        return list;
    }

    public static List<T> FluentClear<T>(this List<T> list)
    {
        list.Clear();
        return list;
    }

    public static List<T> FluentForEach<T>(this List<T> list, Action<T> action)
    {
        list.ForEach(action);
        return list;
    }

    public static List<T> FluentInsert<T>(this List<T> list, int index, T item)
    {
        list.Insert(index, item);
        return list;
    }

    public static List<T> FluentRemoveAt<T>(this List<T> list, int index)
    {
        list.RemoveAt(index);
        return list;
    }

    public static List<T> FluentReverse<T>(this List<T> list)
    {
        list.Reverse();
        return list;
    }
}

internal static void ListFluentExtensions()
{
    var list = new List<int>() { 1, 2, 3, 4, 5 }
        .FluentAdd(1)
        .FluentInsert(0, 0)
        .FluentRemoveAt(1)
        .FluentReverse()
        .FluentForEach(value => value.WriteLine())
        .FluentClear();
}
```

**[⬆ Voltar ao topo](#conteúdo)**

</details>

<details>
  <summary><b>Prefira composição à herança</b></summary>
<br />

Conforme declarado em [_Design Patterns_](https://en.wikipedia.org/wiki/Design_Patterns) pela Gang of Four (GOF), você deve preferir a composição à herança sempre que possível. Existem muitos bons motivos para usar herança e muitos bons motivos para usar composição.

O ponto principal dessa máxima é que se sua mente busca instintivamente a herança, tente pensar se a composição poderia modelar melhor seu problema. Em alguns casos, pode.

Você deve estar se perguntando: "quando devo usar herança?" Isto depende do seu problema em questão, mas esta é uma lista decente de quando a herança faz mais sentido do que a composição:

1. Sua herança representa um relacionamento "é um" e não um relacionamento "tem um" (Humano->Animal vs. Usuário->UserDetails).
2. Você pode reutilizar o código das classes base (os humanos podem se mover como todos os animais).
3. Você deseja fazer alterações globais nas classes derivadas alterando uma classe base (Alterar o gasto calórico de todos os animais quando eles se movem).
<br />

:x: **Errado**

```csharp
class Employee
{
    private string Name { get; set; }
    private string Email { get; set; }

    public Employee(string name, string email)
    {
        Name = name;
        Email = email;
    }

    // ...
}

// Ruim porque os funcionários (Employee) "possuem" dados fiscais (EmployeeTaxData).
// EmployeeTaxData não é um tipo de Employee

class EmployeeTaxData : Employee
{
    private string Name { get; }
    private string Email { get; }

    public EmployeeTaxData(string name, string email, string ssn, string salary)
    {
         // ...
    }

    // ...
}
```

:heavy_check_mark: **Correto**

```csharp
class EmployeeTaxData
{
    public string Ssn { get; }
    public string Salary { get; }

    public EmployeeTaxData(string ssn, string salary)
    {
        Ssn = ssn;
        Salary = salary;
    }

    // ...
}

class Employee
{
    public string Name { get; }
    public string Email { get; }
    public EmployeeTaxData TaxData { get; }

    public Employee(string name, string email)
    {
        Name = name;
        Email = email;
    }

    public void SetTax(string ssn, double salary)
    {
        TaxData = new EmployeeTaxData(ssn, salary);
    }

    // ...
}
```

**[⬆ Voltar ao topo](#conteúdo)**

</details>

## SOLID

<details>
  <summary><b>O que é SOLID?</b></summary>
<br />

**SOLID** é o acrônimo mnemônico (em inglês) introduzido por Michael Feathers para os primeiros cinco princípios nomeados por Robert Martin, que significavam cinco princípios básicos de programação e design orientados a objetos.

- [S: Single Responsibility Principle (SRP) ou Princípio da Responsabilidade Única](#single-responsibility-principle-srp)
- [O: Open/Closed Principle (OCP) ou Princípio Aberto/Fechado](#openclosed-principle-ocp)
- [L: Liskov Substitution Principle (LSP) ou Princípio da Substituição de Liskov](#liskov-substitution-principle-lsp)
- [I: Interface Segregation Principle (ISP) ou Princípio da Segregação de Interfaces](#interface-segregation-principle-isp)
- [D: Dependency Inversion Principle (DIP) ou Princípio da Inversão de Dependência](#dependency-inversion-principle-dip)

</details>

<details>
  <summary><b>Single Responsibility Principle (SRP)</b></summary>
<br />

**Princípio da Responsabilidade Única**
<br />

Conforme declarado no Clean Code, "Nunca deve haver mais de um motivo para a mudança de uma classe". É tentador lotar uma aula com muitas funcionalidades, como quando você só pode levar uma mala no voo. O problema com isso é que sua classe não será conceitualmente coesa e isso lhe dará muitos motivos para mudar. É importante minimizar a quantidade de vezes que você precisa mudar de classe.

É importante porque se houver muita funcionalidade em uma classe e você modificar uma parte dela, pode ser difícil entender como isso afetará outros módulos dependentes em sua base de código.

:x: **Errado**

```csharp
class UserSettings
{
    private User User;

    public UserSettings(User user)
    {
        User = user;
    }

    public void ChangeSettings(Settings settings)
    {
        if (verifyCredentials())
        {
            // ...
        }
    }

    private bool VerifyCredentials()
    {
        // ...
    }
}
```

:heavy_check_mark: **Correto**

```csharp
class UserAuth
{
    private User User;

    public UserAuth(User user)
    {
        User = user;
    }

    public bool VerifyCredentials()
    {
        // ...
    }
}

class UserSettings
{
    private User User;
    private UserAuth Auth;

    public UserSettings(User user)
    {
        User = user;
        Auth = new UserAuth(user);
    }

    public void ChangeSettings(Settings settings)
    {
        if (Auth.VerifyCredentials())
        {
            // ...
        }
    }
}
```

**[⬆ Voltar ao topo](#conteúdo)**

</details>

<details>
  <summary><b>Open/Closed Principle (OCP)</b></summary>
<br />

**Princípio Aberto/Fechado**
<br />

Conforme afirma Bertrand Meyer, “entidades de software (classes, módulos, funções, etc.) devem ser abertas para extensão, mas fechadas para modificação”. O que isso significa? Este princípio basicamente afirma que você deve permitir que os usuários adicionem novas funcionalidades sem alterar o código existente.

:x: **Errado**

```csharp
abstract class AdapterBase
{
    protected string Name;

    public string GetName()
    {
        return Name;
    }
}

class AjaxAdapter : AdapterBase
{
    public AjaxAdapter()
    {
        Name = "ajaxAdapter";
    }
}

class NodeAdapter : AdapterBase
{
    public NodeAdapter()
    {
        Name = "nodeAdapter";
    }
}

class HttpRequester : AdapterBase
{
    private readonly AdapterBase Adapter;

    public HttpRequester(AdapterBase adapter)
    {
        Adapter = adapter;
    }

    public bool Fetch(string url)
    {
        var adapterName = Adapter.GetName();

        if (adapterName == "ajaxAdapter")
        {
            return MakeAjaxCall(url);
        }
        else if (adapterName == "httpNodeAdapter")
        {
            return MakeHttpCall(url);
        }
    }

    private bool MakeAjaxCall(string url)
    {
        // request and return promise
    }

    private bool MakeHttpCall(string url)
    {
        // request and return promise
    }
}
```

:heavy_check_mark: **Correto**

```csharp
interface IAdapter
{
    bool Request(string url);
}

class AjaxAdapter : IAdapter
{
    public bool Request(string url)
    {
        // request and return promise
    }
}

class NodeAdapter : IAdapter
{
    public bool Request(string url)
    {
        // request and return promise
    }
}

class HttpRequester
{
    private readonly IAdapter Adapter;

    public HttpRequester(IAdapter adapter)
    {
        Adapter = adapter;
    }

    public bool Fetch(string url)
    {
        return Adapter.Request(url);
    }
}
```

**[⬆ Voltar ao topo](#conteúdo)**

</details>

<details>
  <summary><b>Liskov Substitution Principle (LSP)</b></summary>
<br />

**Princípio da Substituição de Liskov**
<br />

Este é um termo assustador para um conceito muito simples. É formalmente definido como "Se S é um subtipo de T, então objetos do tipo T podem ser substituídos por objetos do tipo S (ou seja, objetos do tipo S podem substituir objetos do tipo T) sem alterar nenhuma das propriedades desejáveis desse programa (correção, tarefa executada,
etc.)." Essa é uma definição ainda mais assustadora.

A melhor explicação para isso é que se você tiver uma classe pai e uma classe filha, então a classe base e a classe filha podem ser usadas de forma intercambiável sem obter resultados incorretos. Isso ainda pode ser confuso, então vamos dar uma olhada no exemplo clássico do Quadrado-Retângulo. Matematicamente, um quadrado é um retângulo, mas se você modelá-lo usando o relacionamento “é-um” via herança, você rapidamente ter um problema.

:x: **Errado**

```csharp
class Rectangle
{
    protected double Width = 0;
    protected double Height = 0;

    public Drawable Render(double area)
    {
        // ...
    }

    public void SetWidth(double width)
    {
        Width = width;
    }

    public void SetHeight(double height)
    {
        Height = height;
    }

    public double GetArea()
    {
        return Width * Height;
    }
}

class Square : Rectangle
{
    public double SetWidth(double width)
    {
        Width = Height = width;
    }

    public double SetHeight(double height)
    {
        Width = Height = height;
    }
}

Drawable RenderLargeRectangles(Rectangle rectangles)
{
    foreach (rectangle in rectangles)
    {
        rectangle.SetWidth(4);
        rectangle.SetHeight(5);
        var area = rectangle.GetArea(); // BAD: Will return 25 for Square. Should be 20.
        rectangle.Render(area);
    }
}

var rectangles = new[] { new Rectangle(), new Rectangle(), new Square() };
RenderLargeRectangles(rectangles);
```

:heavy_check_mark: **Correto**

```csharp
abstract class ShapeBase
{
    protected double Width = 0;
    protected double Height = 0;

    abstract public double GetArea();

    public Drawable Render(double area)
    {
        // ...
    }
}

class Rectangle : ShapeBase
{
    public void SetWidth(double width)
    {
        Width = width;
    }

    public void SetHeight(double height)
    {
        Height = height;
    }

    public double GetArea()
    {
        return Width * Height;
    }
}

class Square : ShapeBase
{
    private double Length = 0;

    public double SetLength(double length)
    {
        Length = length;
    }

    public double GetArea()
    {
        return Math.Pow(Length, 2);
    }
}

Drawable RenderLargeRectangles(Rectangle rectangles)
{
    foreach (rectangle in rectangles)
    {
        if (rectangle is Square)
        {
            rectangle.SetLength(5);
        }
        else if (rectangle is Rectangle)
        {
            rectangle.SetWidth(4);
            rectangle.SetHeight(5);
        }

        var area = rectangle.GetArea();
        rectangle.Render(area);
    }
}

var shapes = new[] { new Rectangle(), new Rectangle(), new Square() };
RenderLargeRectangles(shapes);
```

**[⬆ Voltar ao topo](#conteúdo)**

</details>

<details>
  <summary><b>Interface Segregation Principle (ISP)</b></summary>
<br />

**Princípio da Segregação de Interfaces**
<br />

O ISP afirma que “os clientes não devem ser forçados a depender de interfaces que não utilizam”.

Um bom exemplo que demonstra esse princípio é para classes que exigem objetos de configurações grandes. Não exigir que os clientes configurem grandes quantidades de opções é benéfico, porque na maioria das vezes eles não precisarão de todas as configurações. Torná-los opcionais ajuda a evitar uma "interface gorda".

:x: **Errado**

```csharp
public interface IEmployee
{
    void Work();
    void Eat();
}

public class Human : IEmployee
{
    public void Work()
    {
        // ....working
    }

    public void Eat()
    {
        // ...... eating in lunch break
    }
}

public class Robot : IEmployee
{
    public void Work()
    {
        //.... working much more
    }

    public void Eat()
    {
        //.... robot can't eat, but it must implement this method
    }
}
```

:heavy_check_mark: **Correto**

Not every worker is an employee, but every employee is an worker.

```csharp
public interface IWorkable
{
    void Work();
}

public interface IFeedable
{
    void Eat();
}

public interface IEmployee : IFeedable, IWorkable
{
}

public class Human : IEmployee
{
    public void Work()
    {
        // ....working
    }

    public void Eat()
    {
        //.... eating in lunch break
    }
}

// robot can only work
public class Robot : IWorkable
{
    public void Work()
    {
        // ....working
    }
}
```

**[⬆ Voltar ao topo](#conteúdo)**

</details>

<details>
  <summary><b>Dependency Inversion Principle (DIP)</b></summary>
<br />

**Princípio de Inversão de Dependência**
<br />

Isso pode ser difícil de entender no início, mas se você trabalhou com a estrutura .NET/.NET Core, viu uma implementação desse princípio na forma de [Injeção de Dependência](https://martinfowler.com/articles/injection.html) (DI). Embora não sejam conceitos idênticos, o DIP impede que os módulos de alto nível conheçam os detalhes de seus módulos de baixo nível e os configurem.
Isso pode ser feito por meio do DI. Um grande benefício disso é que reduz o acoplamento entre os módulos. O acoplamento é um padrão de desenvolvimento muito ruim porque dificulta a refatoração do seu código.

:x: **Errado**

```csharp
public abstract class EmployeeBase
{
    protected virtual void Work()
    {
        // ....working
    }
}

public class Human : EmployeeBase
{
    public override void Work()
    {
        //.... working much more
    }
}

public class Robot : EmployeeBase
{
    public override void Work()
    {
        //.... working much, much more
    }
}

public class Manager
{
    private readonly Robot _robot;
    private readonly Human _human;

    public Manager(Robot robot, Human human)
    {
        _robot = robot;
        _human = human;
    }

    public void Manage()
    {
        _robot.Work();
        _human.Work();
    }
}
```

:heavy_check_mark: **Correto**

```csharp
public interface IEmployee
{
    void Work();
}

public class Human : IEmployee
{
    public void Work()
    {
        // ....working
    }
}

public class Robot : IEmployee
{
    public void Work()
    {
        //.... working much more
    }
}

public class Manager
{
    private readonly IEnumerable<IEmployee> _employees;

    public Manager(IEnumerable<IEmployee> employees)
    {
        _employees = employees;
    }

    public void Manage()
    {
        foreach (var employee in _employees)
        {
            _employee.Work();
        }
    }
}
```

**[⬆ Voltar ao topo](#conteúdo)**

</details>

<details>
  <summary><b>DRY - Don’t repeat yourself (Não repita você mesmo)</b></summary>
<br />

Tente observar o princípio [DRY](https://en.wikipedia.org/wiki/Don%27t_repeat_yourself).

Faça o seu melhor para evitar código duplicado. Código duplicado é ruim porque significa que há mais de um lugar para alterar algo se você precisar alterar alguma lógica.

Imagine se você administra um restaurante e monitora seu estoque: todos os seus tomates, cebolas, alho, temperos, etc. Se você tiver várias listas nas quais mantém isso, todas deverão ser atualizadas quando você servir um prato com tomates neles. Se você tiver apenas uma lista, só há um lugar para atualizar!

Muitas vezes você tem código duplicado porque tem duas ou mais coisas ligeiramente diferentes, que têm muito em comum, mas suas diferenças forçam você a ter duas ou mais funções separadas que fazem muitas das mesmas coisas. Remover código duplicado significa criar uma abstração que possa lidar com esse conjunto de coisas diferentes com apenas uma função/módulo/classe.

Acertar a abstração é fundamental, por isso você deve seguir os princípios SOLID descritos na seção [Classes](#classes). Abstrações ruins podem ser piores que código duplicado, então tome cuidado! Dito isto, se você consegue fazer uma boa abstração, faça-a! Não se repita, caso contrário você se verá atualizando vários lugares sempre que quiser mudar alguma coisa.
<br />

:x: **Errado**

```csharp
public List<EmployeeData> ShowDeveloperList(Developers developers)
{
    List<EmployeeData> listOfEmployeeData = new List<EmployeeData>();

    foreach (var developers in developer)
    {
        var expectedSalary = developer.CalculateExpectedSalary();
        var experience = developer.GetExperience();
        var githubLink = developer.GetGithubLink();

        var employeeData = new EmployeeData(
            expectedSalary,
            experience,
            githubLink
        );

        listOfEmployeeData.Add(employeeData);
    }
}

public List<ManagerData> ShowManagerList(Manager managers)
{
    List<ManagerData> listOfManagerData = new List<ManagerData>();

    foreach (var manager in managers)
    {
        var expectedSalary = manager.CalculateExpectedSalary();
        var experience = manager.GetExperience();
        var githubLink = manager.GetGithubLink();

        var managerData = new ManagerData(
            expectedSalary,
            experience,
            githubLink
        );

        listOfManagerData.Add(managerData);
    }
}
```

:heavy_check_mark: **Correto**

```csharp
public List<EmployeeData> ShowList(Employee employees)
{
    List<EmployeeData> listOfEmployeeData = new List<EmployeeData>();

    foreach (var employee in employees)
    {
        var expectedSalary = employees.CalculateExpectedSalary();
        var experience = employees.GetExperience();
        var githubLink = employees.GetGithubLink();

        var employeeData = new EmployeeData(
            expectedSalary,
            experience,
            githubLink
        );

        listOfEmployeeData.Add(employeeData);
    }
}
```

:heavy_check_mark: **Melhor ainda**

É melhor usar uma versão compacta do código.

```csharp
public List<EmployeeData> ShowList(Employee employees)
{
    List<EmployeeData> listOfEmployeeData = new List<EmployeeData>();

    foreach (var employee in employees)
    {
        listOfEmployeeData.Add(new EmployeeData(
            employee.CalculateExpectedSalary(),
            employee.GetExperience(),
            employee.GetGithubLink()
        ));
    }
}
```

**[⬆ Voltar ao topo](#conteúdo)**

</details>

## Testes

<details>
  <summary><b>Conceito básico de teste</b></summary>
<br />

Teste é mais importante do que o envio do código. Se você não tiver testes ou tiver em quantidade inadequada, toda vez que você enviar o código, você não terá certeza de que não quebrou nada. A decisão sobre o que constitui um valor adequado cabe à sua equipe, mas ter 100% de cobertura (todos os statements e branches) é a maneira que você consegue ter uma confiança muito alta e também dar tranquilidade para o desenvolvedor. Isso significa que além de ter uma ótima estrutura de testes, você também precisa usar uma [boa ferramenta de cobertura](https://docs.microsoft.com/en-us/visualstudio/test/using-code-coverage-to-determine-how-much-code-is-being-tested).

Não há desculpa para não escrever testes. Existem [bons frameworks de teste em .NET](https://github.com/thangchung/awesome-dotnet-core#testing), encontre uma que sua equipe prefira. Quando você encontrar um que funcione para sua equipe, tente sempre escrever testes para cada novo recurso/módulo introduzido. 

Você pode optar também pelo método do _Test Driven Development (TDD)_, que é um bom método para escrever os testes antes mesmo de escrever o código, porém o ponto principal é apenas ter certeza de que você está atingindo seus objetivos de cobertura antes de lançar qualquer recurso ou refatorar um existente.
</details>

<details>
  <summary><b>Conceito de teste por únidade</b></summary>
<br />

Certifique que seus testes sejam focados em uma única coisa e não esteja testando coisas diversas (não relacionadas), force o [padrão AAA](http://wiki.c2.com/?ArrangeActAssert) para tornar seus códigos mais limpos e legíveis.
<br />

:x: **Errado**

```csharp

public class MakeDotNetGreatAgainTests
{
    [Fact]
    public void HandleDateBoundaries()
    {
        var date = new MyDateTime("1/1/2015");
        date.AddDays(30);
        Assert.Equal("1/31/2015", date);

        date = new MyDateTime("2/1/2016");
        date.AddDays(28);
        Assert.Equal("02/29/2016", date);

        date = new MyDateTime("2/1/2015");
        date.AddDays(28);
        Assert.Equal("03/01/2015", date);
    }
}

```

:heavy_check_mark: **Correto**

```csharp

public class MakeDotNetGreatAgainTests
{
    [Fact]
    public void Handle30DayMonths()
    {
        // Arrange
        var date = new MyDateTime("1/1/2015");

        // Act
        date.AddDays(30);

        // Assert
        Assert.Equal("1/31/2015", date);
    }

    [Fact]
    public void HandleLeapYear()
    {
        // Arrange
        var date = new MyDateTime("2/1/2016");

        // Act
        date.AddDays(28);

        // Assert
        Assert.Equal("02/29/2016", date);
    }

    [Fact]
    public void HandleNonLeapYear()
    {
        // Arrange
        var date = new MyDateTime("2/1/2015");

        // Act
        date.AddDays(28);

        // Assert
        Assert.Equal("03/01/2015", date);
    }
}

```

> Fonte: https://www.codingblocks.net/podcast/how-to-write-amazing-unit-tests

**[⬆ Voltar ao topo](#conteúdo)**

</details>

## Concorrência

<details>
  <summary><b>Use Async/Await</b></summary>
<br />

**Resumo das diretrizes de programação assíncrona**

| Nome                     | Descrição                                             | Exceções                        |
| ------------------------ | ----------------------------------------------------- | ------------------------------- |
| Evite `async void`       | Prefira `async Task` em vez de `async void`           | Eventos (Event handlers)        |
| Async por todo o caminho | Não misture código sincrono (bloqueador) e assíncrono | método Console main (C# <= 7.0) |
| Configure o contexto     | Use `ConfigureAwait(false)` sempre que puder          | Métodos que requerem contexto   |

<br />

**O jeito assíncrono de fazer as coisas**

| Para fazer isso ...                                  | Ao invés disso ...           | Use isto             |
| ---------------------------------------------------- | ---------------------------- | -------------------- |
| Recuperar o resultado de uma tarefa em segundo plano | `Task.Wait` ou `Task.Result` | `await`              |
| Aguardar a conclusão de qualquer tarefa              | `Task.WaitAny`               | `await Task.WhenAny` |
| Recuperar os resultados de múltiplas tarefas         | `Task.WaitAll`               | `await Task.WhenAll` |
| Esperar por um período de tempo                      | `Thread.Sleep`               | `await Task.Delay`   |

<br />

**Boas práticas**

O Async/Await é muito bom para tarefas vinculadas a IO (comunicação de rede, comunicação de banco de dados, solicitação http, etc.), mas não é bom para aplicar em tarefas vinculadas computacionalmente (atravessar em uma lista enorme, renderizar uma imagem enorme, etc.) . Porque isso liberará uma thread que está esperando em uma thread pool  a CPU/núcleos disponíveis não envolverão o processamento dessas tarefas. Portanto, devemos evitar o uso de Async/Await para tarefas computacionais vinculadas.

Para lidar com tarefas computacionais, prefira usar `Task.Factory.CreateNew` com `TaskCreationOptions` é `LongRunning`. Ele iniciará uma nova thread em segundo plano para processar uma tarefa computacional pesada sem liberá-la de volta ao pool de threads até que a tarefa seja concluída.

<br />

**Conheça suas ferramentas**

Há muito o que aprender sobre async e await, e é natural ficar um pouco desorientado. Aqui está uma referência rápida de soluções para problemas comuns.

<br />

**Soluções para problemas assíncronos comuns**

| Problema                                                  | Solução                                                                            |
| --------------------------------------------------------- | ---------------------------------------------------------------------------------- |
| Criar uma tarefa para executar código                     | `Task.Run` ou `TaskFactory.StartNew` (não use o construtor `Task` ou `Task.Start`) |
| Criar um wrapper de tarefa para uma operação ou evento    | `TaskFactory.FromAsync` ou `TaskCompletionSource<T>`                               |
| Suporte de cancelamento                                   | `CancellationTokenSource` e `CancellationToken`                                    |
| Reportar progresso                                        | `IProgress<T>` e `Progress<T>`                                                     |
| Lidar com fluxos de dados                                 | TPL Dataflow ou Reactive Extensions                                                |
| Sincronize o acesso a um recurso compartilhado            | `SemaphoreSlim`                                                                    |
| Inicializar um recurso de forma assíncrona                | `AsyncLazy<T>`                                                                     |
| Estruturas de produtor/consumidor prontas para assíncrono | TPL Dataflow or `AsyncCollection<T>`                                               |

<br />

Leia o [documento Padrão Assíncrono Baseado em Tarefas (TAP)](http://www.microsoft.com/download/en/details.aspx?id=19957).
Ele é extremamente bem escrito e inclui orientações sobre design de API e o uso adequado de async/await (incluindo cancelamento e relatórios de progresso).

Existem muitas técnicas novas de espera que devem ser usadas em vez das antigas técnicas de bloqueio. Se você tiver algum desses exemplos antigos em seu novo código assíncrono, você está fazendo isso errado(TM):

| Antigo            | Novo                                 | Descrição                                                 |
| ----------------- | ------------------------------------ | --------------------------------------------------------- |
| `task.Wait`       | `await task`                         | Aguarde a conclusão de uma tarefa                         |
| `task.Result`     | `await task`                         | Obtenha o resultado de uma tarefa concluída               |
| `Task.WaitAny`    | `await Task.WhenAny`                 | Aguarde a conclusão de uma de uma coleção de tarefas      |
| `Task.WaitAll`    | `await Task.WhenAll`                 | Aguarde a conclusão de cada uma de uma coleção de tarefas |
| `Thread.Sleep`    | `await Task.Delay`                   | Aguarde por um período de tempo                           |
| `Task` construtor | `Task.Run` or `TaskFactory.StartNew` | Crie uma tarefa baseada em código                         |

> Fonte https://gist.github.com/jonlabelle/841146854b23b305b50fa5542f84b20c

**[⬆ Voltar ao topo](#conteúdo)**

</details>

## Tratamento de Erros (Error Handling)

<details>
  <summary><b>Conceito básico de tratamento de erros</b></summary>
<br />

Lançar erros é uma coisa boa! Significa que o tempo de execução identificou com sucesso quando algo deu errado em seu programa e está lhe informando interrompendo a execução da função na pilha atual, encerrando todo o processo (no .NET/.NET Core) e notificando você no console com um rastreamento de pilha.

</details>

<details>
  <summary><b>Não use 'throw ex' no bloco catch</b></summary>
<br />

Se você precisar lançar novamente uma exceção depois de capturá-la, use apenas 'throw'. Ao usar isso, você preservará o rastreamento de pilha.<br />
Se você fizer como na opção errada abaixo, você perderá o rastreamento de pilha.
<br />

:x: **Errado**

```csharp
try
{
    // Do something..
}
catch (Exception ex)
{
    // Any action something like roll-back or logging etc.
    throw ex;
}
```

:heavy_check_mark: **Correto**

```csharp
try
{
    // Do something..
}
catch (Exception ex)
{
    // Any action something like roll-back or logging etc.
    throw;
}
```

**[⬆ Voltar ao topo](#conteúdo)**

</details>

<details>
  <summary><b>Não ignore os erros capturados</b></summary>
<br />

Não fazer nada com um erro detectado não lhe dá a capacidade de corrigir ou reagir a esse erro. Lançar o erro não é muito melhor, pois muitas vezes ele pode se perder em um mar de coisas impressas no console. Se você agrupar qualquer pedaço de código em um `try/catch` significa que você acha que um erro pode ocorrer ali e, portanto, você deve ter um plano, ou criar um caminho de código, para quando isso ocorrer.
<br />

:x: **Errado**

```csharp
try
{
    FunctionThatMightThrow();
}
catch (Exception ex)
{
    // silent exception
}
```

:heavy_check_mark: **Correto**

```csharp
try
{
    FunctionThatMightThrow();
}
catch (Exception error)
{
    NotifyUserOfError(error);

    // Another option
    ReportErrorToService(error);
}
```

**[⬆ Voltar ao topo](#conteúdo)**

</details>

<details>
  <summary><b>Use vários blocos catch em vez de condições if.</b></summary>
<br />

Se você precisar tomar medidas de acordo com o tipo de exceção, é melhor você usar vários blocos `catch` para tratamento de exceções.
<br />

:x: **Errado**

```csharp
try
{
    // Do something..
}
catch (Exception ex)
{

    if (ex is TaskCanceledException)
    {
        // Take action for TaskCanceledException
    }
    else if (ex is TaskSchedulerException)
    {
        // Take action for TaskSchedulerException
    }
}
```

:heavy_check_mark: **Correto**

```csharp
try
{
    // Do something..
}
catch (TaskCanceledException ex)
{
    // Take action for TaskCanceledException
}
catch (TaskSchedulerException ex)
{
    // Take action for TaskSchedulerException
}
```

**[⬆ Voltar ao topo](#conteúdo)**

</details>

<details>
  <summary><b>Mantenha o rastreamento da pilha de exceções ao relançar exceções</b></summary>
<br />

C# permite que a exceção seja lançada novamente em um bloco catch usando a palavra-chave `throw`. É uma má prática lançar uma exceção capturada usando `throw ex;`. Esta instrução redefine o rastreamento de pilha. Em vez disso, use `throw;`. Isso manterá o rastreamento de pilha e fornecerá uma visão mais profunda sobre a exceção.<br />

Outra opção é usar uma exceção personalizada. Simplesmente instancie uma nova exceção e defina sua propriedade de exceção interna para a exceção capturada com throw `new CustomException("some info", ex);`. <br />

Adicionar informações a uma exceção é uma boa prática, pois ajudará na depuração. No entanto, se o objetivo é registrar uma exceção, use `throw;` para passar a responsabilidade para o chamador.
<br />

:x: **Errado**

```csharp
try
{
    FunctionThatMightThrow();
}
catch (Exception ex)
{
    logger.LogInfo(ex);
    throw ex;
}
```

:heavy_check_mark: **Correto**

```csharp
try
{
    FunctionThatMightThrow();
}
catch (Exception error)
{
    logger.LogInfo(error);
    throw;
}
```

:heavy_check_mark: **Correto**

```csharp
try
{
    FunctionThatMightThrow();
}
catch (Exception error)
{
    logger.LogInfo(error);
    throw new CustomException(error);
}
```

**[⬆ Voltar ao topo](#conteúdo)**

</details>

<details>
  <summary><b>Use exceção contextualizada em vez do objeto 'Exception'</b></summary>
<br />

Sempre que possível, lance exceções contextualizadas em vez de usar a exceção padrão.
<br />

:x: **Errado**

```csharp
public double Divide(double dividend, double divider) {
    if (divider == 0)
    {
        throw new Exception("Cannot be divided by zero");
    }

    return dividend / divider;
}
```

:heavy_check_mark: **Correto**

```csharp
public double Divide(double dividend, double divider) {
    if (divider == 0)
    {
        throw new InvalidOperationException("Cannot be divided by zero");
    }

    return dividend / divider;
}
```

**[⬆ Voltar ao topo](#conteúdo)**

</details>

## Formatação

<details>
  <summary><b>Use o arquivo <i>.editorconfig</i></b></summary>
<br />

:x: **Errado**
<br />

Possuir muitos estilos de formatação de código no projeto. Por exemplo, o estilo de recuo é `space` e `tab` misturados no projeto.
<br />

:heavy_check_mark: **Correto**
<br />

Defina e mantenha um estilo de código consistente em sua base de código com o uso de um arquivo `.editorconfig`
<br />

```csharp
root = true

[*]
indent_style = space
indent_size = 2
end_of_line = lf
charset = utf-8
trim_trailing_whitespace = true
insert_final_newline = true

# C# files
[*.cs]
indent_size = 4
# New line preferences
csharp_new_line_before_open_brace = all
csharp_new_line_before_else = true
csharp_new_line_before_catch = true
csharp_new_line_before_finally = true
csharp_new_line_before_members_in_object_initializers = true
csharp_new_line_before_members_in_anonymous_types = true
csharp_new_line_within_query_expression_clauses = true

# Code files
[*.{cs,csx,vb,vbx}]
indent_size = 4

# Indentation preferences
csharp_indent_block_contents = true
csharp_indent_braces = false
csharp_indent_case_contents = true
csharp_indent_switch_labels = true
csharp_indent_labels = one_less_than_current

# avoid this. unless absolutely necessary
dotnet_style_qualification_for_field = false:suggestion
dotnet_style_qualification_for_property = false:suggestion
dotnet_style_qualification_for_method = false:suggestion
dotnet_style_qualification_for_event = false:suggestion

# only use var when it's obvious what the variable type is
# csharp_style_var_for_built_in_types = false:none
# csharp_style_var_when_type_is_apparent = false:none
# csharp_style_var_elsewhere = false:suggestion

# use language keywords instead of BCL types
dotnet_style_predefined_type_for_locals_parameters_members = true:suggestion
dotnet_style_predefined_type_for_member_access = true:suggestion

# name all constant fields using PascalCase
dotnet_naming_rule.constant_fields_should_be_pascal_case.severity = suggestion
dotnet_naming_rule.constant_fields_should_be_pascal_case.symbols  = constant_fields
dotnet_naming_rule.constant_fields_should_be_pascal_case.style    = pascal_case_style

dotnet_naming_symbols.constant_fields.applicable_kinds   = field
dotnet_naming_symbols.constant_fields.required_modifiers = const

dotnet_naming_style.pascal_case_style.capitalization = pascal_case

# static fields should have s_ prefix
dotnet_naming_rule.static_fields_should_have_prefix.severity = suggestion
dotnet_naming_rule.static_fields_should_have_prefix.symbols  = static_fields
dotnet_naming_rule.static_fields_should_have_prefix.style    = static_prefix_style

dotnet_naming_symbols.static_fields.applicable_kinds   = field
dotnet_naming_symbols.static_fields.required_modifiers = static

dotnet_naming_style.static_prefix_style.required_prefix = s_
dotnet_naming_style.static_prefix_style.capitalization = camel_case

# internal and private fields should be _camelCase
dotnet_naming_rule.camel_case_for_private_internal_fields.severity = suggestion
dotnet_naming_rule.camel_case_for_private_internal_fields.symbols  = private_internal_fields
dotnet_naming_rule.camel_case_for_private_internal_fields.style    = camel_case_underscore_style

dotnet_naming_symbols.private_internal_fields.applicable_kinds = field
dotnet_naming_symbols.private_internal_fields.applicable_accessibilities = private, internal

dotnet_naming_style.camel_case_underscore_style.required_prefix = _
dotnet_naming_style.camel_case_underscore_style.capitalization = camel_case

# Code style defaults
dotnet_sort_system_directives_first = true
csharp_preserve_single_line_blocks = true
csharp_preserve_single_line_statements = false

# Expression-level preferences
dotnet_style_object_initializer = true:suggestion
dotnet_style_collection_initializer = true:suggestion
dotnet_style_explicit_tuple_names = true:suggestion
dotnet_style_coalesce_expression = true:suggestion
dotnet_style_null_propagation = true:suggestion

# Expression-bodied members
csharp_style_expression_bodied_methods = false:none
csharp_style_expression_bodied_constructors = false:none
csharp_style_expression_bodied_operators = false:none
csharp_style_expression_bodied_properties = true:none
csharp_style_expression_bodied_indexers = true:none
csharp_style_expression_bodied_accessors = true:none

# Pattern matching
csharp_style_pattern_matching_over_is_with_cast_check = true:suggestion
csharp_style_pattern_matching_over_as_with_null_check = true:suggestion
csharp_style_inlined_variable_declaration = true:suggestion

# Null checking preferences
csharp_style_throw_expression = true:suggestion
csharp_style_conditional_delegate_call = true:suggestion

# Space preferences
csharp_space_after_cast = false
csharp_space_after_colon_in_inheritance_clause = true
csharp_space_after_comma = true
csharp_space_after_dot = false
csharp_space_after_keywords_in_control_flow_statements = true
csharp_space_after_semicolon_in_for_statement = true
csharp_space_around_binary_operators = before_and_after
csharp_space_around_declaration_statements = do_not_ignore
csharp_space_before_colon_in_inheritance_clause = true
csharp_space_before_comma = false
csharp_space_before_dot = false
csharp_space_before_open_square_brackets = false
csharp_space_before_semicolon_in_for_statement = false
csharp_space_between_empty_square_brackets = false
csharp_space_between_method_call_empty_parameter_list_parentheses = false
csharp_space_between_method_call_name_and_opening_parenthesis = false
csharp_space_between_method_call_parameter_list_parentheses = false
csharp_space_between_method_declaration_empty_parameter_list_parentheses = false
csharp_space_between_method_declaration_name_and_open_parenthesis = false
csharp_space_between_method_declaration_parameter_list_parentheses = false
csharp_space_between_parentheses = false
csharp_space_between_square_brackets = false

[*.{asm,inc}]
indent_size = 8

# Xml project files
[*.{csproj,vcxproj,vcxproj.filters,proj,nativeproj,locproj}]
indent_size = 2

# Xml config files
[*.{props,targets,config,nuspec}]
indent_size = 2

[CMakeLists.txt]
indent_size = 2

[*.cmd]
indent_size = 2

```

**[⬆ Voltar ao topo](#conteúdo)**

</details>

## Comentários

<details>
  <summary><b>Evite marcadores posicionais</b></summary>
<br />

Eles geralmente apenas adicionam ruído. Deixe que as funções e os nomes das variáveis, juntamente com o recuo e a formatação adequados, forneçam a estrutura visual ao seu código.
<br />

:x: **Errado**

```csharp
////////////////////////////////////////////////////////////////////////////////
// Scope Model Instantiation
////////////////////////////////////////////////////////////////////////////////
var model = new[]
{
    menu: 'foo',
    nav: 'bar'
};

////////////////////////////////////////////////////////////////////////////////
// Action setup
////////////////////////////////////////////////////////////////////////////////
void Actions()
{
    // ...
};
```

:x: **Errado**

```csharp

#region Scope Model Instantiation

var model = {
    menu: 'foo',
    nav: 'bar'
};

#endregion

#region Action setup

void Actions() {
    // ...
};

#endregion
```

:heavy_check_mark: **Correto**

```csharp
var model = new[]
{
    menu: 'foo',
    nav: 'bar'
};

void Actions()
{
    // ...
};
```

**[⬆ Voltar ao topo](#conteúdo)**

</details>

<details>
  <summary><b>Não deixe código comentado em sua base de código</b></summary>
<br />

O controle de versão existe por um motivo. Deixe o código antigo em seu histórico.
<br />

:x: **Errado**

```csharp
doStuff();
// doOtherStuff();
// doSomeMoreStuff();
// doSoMuchStuff();
```

:heavy_check_mark: **Correto**

```csharp
doStuff();
```

**[⬆ Voltar ao topo](#conteúdo)**

</details>

<details>
  <summary><b>Não tenho histórico de comentários</b></summary>
<br />

Lembre-se, use o controle de versão! Não há necessidade de código morto, código comentado e, especialmente, histórico de comentários. <br />
Use `git log` para obter o histórico!
<br />

:x: **Errado**

```csharp
/**
 * 2018-12-20: Removed monads, didn't understand them (RM)
 * 2017-10-01: Improved using special monads (JP)
 * 2016-02-03: Removed type-checking (LI)
 * 2015-03-14: Added combine with type-checking (JR)
 */
public int Combine(int a,int b)
{
    return a + b;
}
```

:heavy_check_mark: **Correto**

```csharp
public int Combine(int a,int b)
{
    return a + b;
}
```

**[⬆ Voltar ao topo](#conteúdo)**

</details>

<details>
  <summary><b>Comente apenas coisas que tenham complexidade de lógica de negócios</b></summary>
<br />

Os comentários são um pedido de desculpas, não um requisito. Um bom código _principalmente_ documenta a si mesmo.
<br />

:x: **Errado**

```csharp
public int HashIt(string data)
{
    // The hash
    var hash = 0;

    // Length of string
    var length = data.length;

    // Loop through every character in data
    for (var i = 0; i < length; i++)
    {
        // Get character code.
        const char = data.charCodeAt(i);
        // Make the hash
        hash = ((hash << 5) - hash) + char;
        // Convert to 32-bit integer
        hash &= hash;
    }
}
```

**Melhor, mas ainda incorreto**

```csharp
public int HashIt(string data)
{
    var hash = 0;
    var length = data.length;
    for (var i = 0; i < length; i++)
    {
        const char = data.charCodeAt(i);
        hash = ((hash << 5) - hash) + char;

        // Convert to 32-bit integer
        hash &= hash;
    }
}
```

Se um comentário explica O QUE o código está fazendo, provavelmente é um comentário inútil e pode ser implementado com uma variável ou função bem nomeada. O comentário no código anterior poderia ser substituído por uma função chamada `ConvertTo32bitInt`, portanto este comentário ainda é inútil.
No entanto, seria difícil expressar por código POR QUE o desenvolvedor escolheu o algoritmo hash djb2 em vez de sha-1 ou outra função hash. Nesse caso, um comentário é aceitável.

:heavy_check_mark: **Correto**

```csharp
public int Hash(string data)
{
    var hash = 0;
    var length = data.length;

    for (var i = 0; i < length; i++)
    {
        var character = data[i];
        // use of djb2 hash algorithm as it has a good compromise
        // between speed and low collision with a very simple implementation
        hash = ((hash << 5) - hash) + character;

        hash = ConvertTo32BitInt(hash);
    }
    return hash;
}

private int ConvertTo32BitInt(int value)
{
    return value & value;
}
```

**[⬆ Voltar ao topo](#conteúdo)**

</details>

# Outros Recursos de Clean Code

## Outras listas de Clean Code

- [clean-code-javascript](https://github.com/felipe-augusto/clean-code-javascript) - Conceitos Clean Code adaptado para JavaScript
- [clean-code-php](https://github.com/jupeter/clean-code-php) - Conceitos Clean Code adaptado para PHP
- [clean-code-ruby](https://github.com/uohzxela/clean-code-ruby) - Conceitos Clean Code adaptado para Ruby
- [clean-code-python](https://github.com/zedr/clean-code-python) - Conceitos Clean Code adaptado para Python
- [clean-code-typescript](https://github.com/labs42io/clean-code-typescript) - Conceitos Clean Code adaptado para TypeScript
- [clean-go-article](https://github.com/Pungyeon/clean-go-article) - Conceitos Clean Code adaptado para Golang e um examplo de como aplicar [clean code in Golang](https://github.com/Pungyeon/clean-go)
- [clean-abap](https://github.com/SAP/styleguides) - Conceitos Clean Code adaptado para ABAP
- [programming-principles](https://github.com/webpro/programming-principles) - Visão geral categorizada de princípios e padrões de programação
- [Elixir-Code-Smells](https://github.com/lucasvegi/Elixir-Code-Smells) - Catálogo de code smells específicos do Elixir
- [awesome-clean-code](https://github.com/kkisiele/awesome-clean-code) - Princípios de design, artigos em destaque, tutoriais, vídeos, exemplos de código, blogs e livros

## Guia de Estilos
- [Google Styleguides](https://github.com/google/styleguide) - Este projeto contém o Guia de Estilo C++, Guia de Estilo Swift, Guia de Estilo Objective-C, Guia de Estilo Java, Guia de Estilo Python, Guia de Estilo R, Guia de Estilo Shell, Guia de Estilo HTML/CSS, Guia de Estilo JavaScript, Guia de Estilo AngularJS, Common Lisp Guia de estilo e guia de estilo Vimscript
- [Django Styleguide](https://github.com/HackSoftware/Django-Styleguide) - Guia de estilo Django usado em projetos HackSoft

## Ferramentas

- [codemaid](https://github.com/codecadwallader/codemaid) - Extensão de código aberto do Visual Studio para limpar e simplificar nossa codificação C#, C++, F#, VB, PHP, PowerShell, JSON, XAML, XML, ASP, HTML, CSS, LESS, SCSS, JavaScript e TypeScript
- [Sharpen](https://github.com/sharpenrocks/Sharpen) - Extensão do Visual Studio que introduz de forma inteligente novos recursos C# em sua base de código existente
- [tslint-clean-code](https://github.com/Glavin001/tslint-clean-code) - Regras TSLint para aplicar Código Limpo

## Cheatsheets

- [AspNetCoreDiagnosticScenarios](https://github.com/davidfowl/AspNetCoreDiagnosticScenarios) - Exemplos de broken patterns em aplicativos ASP.NET Core
- [Clean Code](cheatsheets/Clean-Code-V2.4.pdf) - Um resumo do livro [Código limpo: habilidades práticas do Agile software](https://www.amazon.com.br/dp/8576082675?ref_=cm_sw_r_cp_ud_dp_AHQYXKPJZ8ECWCBN8ZWK)
- [Clean Architecture](cheatsheets/Clean-Architecture-V1.0.pdf) - Um resumo do livro [Arquitetura limpa: o guia do artesão para estrutura e design de software](https://www.amazon.com.br/dp/8550804606?ref_=cm_sw_r_cp_ud_dp_JVE09W25S10GF7Y62ZC3)
- [Modern JavaScript Cheatsheet](https://github.com/mbeaudru/modern-js-cheatsheet) - Cheatsheet para o conhecimento de JavaScript que você encontrará frequentemente em projetos modernos
- [OWASP Cheat Sheet Series](https://cheatsheetseries.owasp.org) - Cheatsheet foi criado para fornecer uma coleção concisa de informações de alto valor sobre tópicos específicos de segurança de aplicativos
- [.NET Memory Performance Analysis](https://github.com/Maoni0/mem-doc/blob/master/doc/.NETMemoryPerformanceAnalysis.md) - Este documento tem como objetivo ajudar as pessoas que desenvolvem aplicativos em .NET a pensar sobre a análise de desempenho de memória e a encontrar as abordagens corretas para realizar tal análise, se necessário. Neste contexto, o .NET inclui o .NET Framework e o .NET Core. Para obter as melhorias de memória mais recentes no coletor de lixo e no restante da estrutura, recomendo fortemente que você esteja no .NET Core, caso ainda não esteja, porque é onde o desenvolvimento ativo acontece
- [naming-cheatsheet](https://github.com/kettanaito/naming-cheatsheet) - Diretrizes abrangentes e independentes de linguagem sobre nomenclatura de variáveis
- [101 Design Patterns & Tips for Developers](https://sourcemaking.com/design-patterns-and-tips)
- [Go Concurrency Guide](https://github.com/luk4z7/go-concurrency-guide)

---
