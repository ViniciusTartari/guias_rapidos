# Princípios S.O.L.I.D. utilizando Typescript

**SOLID** é um acrônimo para os cinco primeiros princípios de design orientado a objetos (OOD) de Robert C. Martin, conhecido popularmente como @UncleBob.

Os cinco princípios **SOLID** são:

- **S**ingle responsibility principle (princípio da responsabilidade única): uma classe deve ter um e apenas um motivo para mudar;
- **O**pen-closed principle (Princípio aberto-fechado): deve ser possível estender o comportamento de uma classe sem modificá-lo;
- **L**iskov Substitution principle(Princípio Liskov de substituição): subclasses devem ser substituíveis por suas superclasses;
- **I**nterface segregation principle (Princípio de segregação de interface): muitas interfaces pequenas e específicas do cliente são melhores que uma interface de uso geral;
- **D**ependency inversion principle (Princípio de inversão de dependência): depende de abstrações, não de concreções;

Esses princípios facilitam o desenvolvimento de um software fácil de manter e estender. Eles também facilitam para os desenvolvedores evitar código de perfumaria, refatoração de código e são também uma parte do desenvolvimento ágil ou adaptativa de software.

## The Single Responsibility Principle (SRP)

O **SRP** exige que uma classe tenha apenas um motivo para mudar. Uma classe que segue esse princípio executa apenas algumas tarefas relacionadas. Você não precisa limitar seu pensamento às classes ao considerar o **SRP**. Você pode aplicar o princípio a métodos ou módulos, garantindo que eles façam apenas uma coisa e, portanto, tenham apenas um motivo para mudar.

### Exemplo

#### Forma incorreta

A classe _Task_ define propriedades relacionadas ao modelo, mas também define o método de acesso a dados para salvar a entidade em uma fonte de dados genérica:

```typescript
/*
 * Esta classe nao segue o principio SRP
 */
class Task {
  private db: Database;

  constructor(private title: string, private deadline: Date) {
    this.db = Database.connect("admin:password@fakedb", ["tasks"]);
  }

  getTitle() {
    return this.title + "(" + this.deadline + ")";
  }
  save() {
    this.db.tasks.save({ title: this.title, date: this.deadline });
  }
}
```

#### Forma correta

A classe _Task_ pode ser dividida entre a classe _Task_, que cuida da descrição do modelo e do _TaskRepository_, responsável por armazenar os dados.

```typescript
/*
 * Esta classe segue o principio SRP
 */
class Task {
  constructor(private title: string, private deadline: Date) {}

  getTitle() {
    return this.title + "(" + this.deadline + ")";
  }
}

class TaskRepository {
  private db: Database;

  constructor() {
    this.db = Database.connect("admin:password@fakedb", ["tasks"]);
  }

  save(task: Task) {
    this.db.tasks.save(JSON.stringify(task));
  }
}
```

## The Open-closed Princple (OCP)

    As entidades de software devem estar abertas para extensão, mas fechadas para modificação.

O risco de alterar uma classe existente é que você introduzirá uma alteração inadvertida no comportamento. A solução é criar outra classe que substitua o comportamento da classe original. Seguindo o OCP, é mais provável que um componente contenha código sustentável e reutilizável.

### Exemplo

A classe _CreditCard_ descreve um método para calcular o _MonthlyDiscount()_. O _MonthlyDiscount()_ depende do tipo de cartão, que pode ser: prata ou ouro. Para alterar o cálculo do desconto mensal, você deve criar outra classe que substitua o método _MonthlyDiscount()_.

A solução é criar duas novas classes: uma para cada tipo de cartão.

```typescript
class CreditCard {
  private Code: String;
  private Expiration: Date;
  protected MonthlyCost: number;

  constructor(code: String, Expiration: Date, MonthlyCost: number) {
    this.Code = code;
    this.Expiration = Expiration;
    this.MonthlyCost = MonthlyCost;
  }

  getCode(): String {
    return this.Code;
  }

  getExpiration(): Date {
    return this.Expiration;
  }

  monthlyDiscount(): number {
    return this.MonthlyCost * 0.02;
  }
}

class GoldCreditCard extends CreditCard {
  monthlyDiscount(): number {
    return this.MonthlyCost * 0.05;
  }
}

class SilverCreditCard extends CreditCard {
  monthlyDiscount(): number {
    return this.MonthlyCost * 0.03;
  }
}
```

## The Liskov Substitution Principle (LSP)

    As classes filho nunca devem quebrar as definições de tipo da classe pai.

O conceito desse princípio foi introduzido por Barbara Liskov em uma palestra de conferência em 1987 e posteriormente publicada em um artigo junto com Jannette Wing em 1994.

Tão simples como isso, uma subclasse deve substituir os métodos da classe pai de uma maneira que não quebre a funcionalidade do ponto de vista de um cliente.

### Exemplo

No exemplo a seguir _ItalyPostalAddress_, _UKPostalAddress_ e _USAPostalAddress_ estendem uma classe comum: _PostalAddress_.

A classe _AddressWriter_ refere-se _PostalAddress_: o parâmetro _writer_ pode ser de três subtipos diferentes.

```typescript
abstract class PostalAddress {
  Addressee: string;
  Country: string;
  PostalCode: string;
  City: string;
  Street: string;
  House: number;

  /*
   * @returns Formatted full address
   */
  abstract WriteAddress(): string;
}

class ItalyPostalAddress extends PostalAddress {
  WriteAddress(): string {
    return "Formatted Address Italy" + this.City;
  }
}
class UKPostalAddress extends PostalAddress {
  WriteAddress(): string {
    return "Formatted Address UK" + this.City;
  }
}
class USAPostalAddress extends PostalAddress {
  WriteAddress(): string {
    return "Formatted Address USA" + this.City;
  }
}

class AddressWriter {
  PrintPostalAddress(writer: PostalAddress): string {
    return writer.WriteAddress();
  }
}
```

## The Interface Segregation Principle (ISP)

É bastante comum descobrir que uma interface é, essencialmente, apenas uma descrição de uma classe inteira. O ISP afirma que devemos escrever uma série de interfaces menores e mais específicas que são implementadas pela classe. Cada interface fornece um único comportamento.

### Exemplo

#### Forma incorreta

A seguinte interface da impressora torna impossível implementar uma impressora que pode imprimir e copiar, mas não grampear:

```typescript
interface Printer {
  copyDocument();
  printDocument(document: Document);
  stapleDocument(document: Document, tray: Number);
}

class SimplePrinter implements Printer {
  public copyDocument() {
    //...
  }

  public printDocument(document: Document) {
    //...
  }

  public stapleDocument(document: Document, tray: Number) {
    //...
  }
}
```

#### Forma correta

O exemplo a seguir mostra uma abordagem alternativa que agrupa métodos em interfaces mais específicas. Ele descreve vários contratos que podem ser implementados individualmente por uma impressora simples ou copiadora simples ou por uma super impressora:

```typescript
interface Printer {
  printDocument(document: Document);
}

interface Stapler {
  stapleDocument(document: Document, tray: number);
}

interface Copier {
  copyDocument();
}

class SimplePrinter implements Printer {
  public printDocument(document: Document) {
    //...
  }
}

class SuperPrinter implements Printer, Stapler, Copier {
  public copyDocument() {
    //...
  }

  public printDocument(document: Document) {
    //...
  }

  public stapleDocument(document: Document, tray: number) {
    //...
  }
}
```

## The Dependency inversion principle (DIP)

O DIP simplesmente declara que as classes de alto nível não devem depender de componentes de baixo nível, mas sim de uma abstração.

### Exemplo

#### Forma incorreta

O _WindowSwitch_ de alto nível depende da classe _CarWindow_ de nível inferior:

```typescript
class CarWindow {
  open() {
    //...
  }

  close() {
    //...
  }
}

class WindowSwitch {
  private isOn = false;

  constructor(private window: CarWindow) {}

  onPress() {
    if (this.isOn) {
      this.window.close();
      this.isOn = false;
    } else {
      this.window.open();
      this.isOn = true;
    }
  }
}
```

#### Forma correta

Para seguir o DIP, a classe _WindowSwitch_ deve referenciar uma interface (_IWindow_) implementada pelo objeto _CarWindow_:

```typescript
interface IWindow {
  open();
  close();
}

class CarWindow implements IWindow {
  open() {
    //...
  }

  close() {
    //...
  }
}

class WindowSwitch {
  private isOn = false;

  constructor(private window: IWindow) {}

  onPress() {
    if (this.isOn) {
      this.window.close();
      this.isOn = false;
    } else {
      this.window.open();
      this.isOn = true;
    }
  }
}
```

## Conclusão

O typescript possibilita trazer todos os princípios e práticas do OOP para o seu software, usando os princípios do **SOLID** para guiar seus padrões de design.
