Angular 4 - Notları
====================

Çevirmen Notu: Notların sahibi ve bu reponun orjinaline sahip olan [co3moz](https://github.com/co3moz)'a linkten ulaşabilirsiniz. Bu repo ingilizce problemi olan arkadaşların da bu notlardan faydalanabilmesi için Türkçe'ye çevrilmiştir.

Teknik olarak çevirilmemesinin daha doğru olacağını düşündüğüm tabirleri (Input, Output, View, Encapsulation, Databinding) çevirmemeyi tercih ettim. Çünkü bu tabirlerle sorun yaşadığınızda tüm kaynaklarda bu şekilde geçecekler. Onun dışında çeviri hataları varsa her türlü katkıya açık olan bu repoya pr atabilirsiniz.

Bu kod deposu benim angular 4 notlarımın bir derlemesidir. Angular 2'yi deneyememiştim. Fakat şimdi Angular 4'e bir göz atmaya ve bir ders hazırlamaya karar verdim. Öğrendiğim her şeyi yazacağım, belki bu kod deposu sizin için de rehber olabilir.

[Maximilian Schwarzmuller](https://www.udemy.com/the-complete-guide-to-angular-2)'e bu harika rehber için teşekkürler.


İçindekiler
----------------

- [Kurulum](#installation)
- [Bir proje yaratmak](#creating-project)
- [Projeyi çalıştırmak](#serving-project)
- [Çalıştırılmış Projeyi İncelemek](#investigating-created-project)
- [Yeni bir komponent oluşturmak](#creating-a-new-component)
- [Komut satırı ile bir komponent oluşturmak](#create-component-with-cli)
- [Projeye bootstrap css eklemek](#including-bootstrap-css-to-project)
- [Databinding](#databinding)
- [Direktifler](#directives)
  - [ngIf](#ngif)
  - [ngFor](#ngfor)
  - [ngStyle](#ngstyle)
  - [ngClass](#ngclass)
  - [ngSwitch](#ngswitch)
- [Input](#input)
- [Output](#output)
- [View Encapsulation](#view-encapsulation)
- [Yerel Referanslar](#local-reference)
- [ng-content](#ng-content)
- [Komponentlerin Yaşam Döngüsü](#life-cycle-of-components)
- [Yeni bir direktif oluşturmak](#creating-a-new-directive)
  - [HostListener](#hostlistener)
  - [HostBinding](#hostbinding)
- [Servisler ve Bağlılıkların Zerki](#services-and-dependency-injection)
  - [Bir servisi bir başka servise zerk etmek](#injecting-a-service-into-another-service)
  - [Olay yayınlama servisi](#event-emitting-service)
- [Rotalar](#router)
  - [Linkler](#links)
  - [Aktif Roota](#active-route)
  - [Kod içinden yönlendirme](#navigating-from-code)
  - [Rota parametreleri](#parameters-of-routes)
  - [Birleşik Rotalar](#nested-routes)
  - [Yönlendirme](#redirecting)

### Kurulum

Uygulama geliştirmek için ilk önce node.js kurmamız gerekiyor. Eğer node.js nedir bilmiyorsanız Angular 4'ten önce lütfen ona bir göz atın. Biz angular komut satırı eklentisini kullanacağız, bu eklenti bize projelerimizi yaratırken yardımcı olacak. Oldukça kullanışlı bir araç.

```
npm i @angular/cli -g
```

Angular komut satırı paketini `@angular/cli` global parametresiyle yüklemeliyiz. Bu parametre proje lokaline değil global node_modules klasörüne kurulum sağlayacaktır. 

Artık terminalde `ng` komutunu kullanabiliyor olmamız gerek.

### Proje yaratmak

Proje yaratmak için `ng` komutunu kullanacağız. Eğer terminale `ng` yazdığınızda bir hata alıyorsanız `Kurulum` adımında bir hata yapmışsınız demektir, lütfen o adıma gidip işlemleri doğru şekilde tamamladığınızdan emin olun. 

`ng` komutu birden fazla opsiyonel parametreye sahiptir. O konuya da geleceğiz ancak öncelikle bir proje yaratmak için `new` parametresini kullanmalıyız.

Bu parametre güncel dizinimizde yeni bir proje yapısı oluşturacaktır. Ancak işlem sırasında bir proje ismi vermeliyiz. Ben proje ismi olarak ilk uygulamam anlamına gelen "my-first-app" ismini seçtim.

```
ng new my-first-app
```

Bu komutu kullandıktan sonra terminalimiz `ng` tarafından bazı dosyalar oluşturacak. Ardından gerekli npm paketlerini yükleyecek, işlemler tamamlanana kadar bekleyin.

### Projeyi çalıştırmak

Az önce yeni bir proje oluşturduk. `my-first-app` klasörüne girip `ng` nin `serve` komutunu kullanırsak yüklenen paketler bir http sunucusu oluşturup yayına başlayacaktır.

```
cd my-first-app
ng serve
```

Terminal çıktımızda bir url adresi olmalı. İsterseniz seçiminize bağlı olarak `--port xx` parametresiyle uygulamanın istediğiniz herhangi bir porttan yayınlanmasını sağlayabilirsiniz.

```
ng serve --port 8080
```

Typescript javascript'e çevrildi ve Webpack uygulamanızı paketledi.
Artık localhost:8080 adresnden uygulamaya erişebilirsiniz.


### Çalıştırılmış Projeyi İncelemek

> Daha fazla derinlere inmeden önce projeyi bir IDE ile açtığınızdan emin olun. Ben Visual Studio Code ya da WebStorm tavsiye ediyorum.

Proje dizininde `e2e` klasörünü, `src` klasörünü ve birkaç dosyayı göreceğiz. `e2e` klasörünü uçtan uca testleri içerir. Buna daha sonra göz atacağız. (Testlerin kaderi bu.) Projemizin tüm kaynak dosyaları `src` klasöründe bulunur. Diğer dosyalar da proje konfigürasyonlarıyla ilgili bilgileri, paket bağımlılıklarını ve benzeri detayları içerirler. İhtiyaç duyduğumuzda onlarla tekrar ilgileneceğiz.

`src` klasörünün içinde birden fazla dosya var. Bu dizindeki en önemli dosya `index.html` dosyası. Bu dosya projemizin en üst noktası. Eğer dosyayı açarsanız aşağıdaki gibi olduğunu göreceksiniz.


```html
<!doctype html>
<html>
<head>
    <meta charset="utf-8">
    <title>MyFirstApp</title>
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <link rel="icon" type="image/x-icon" href="favicon.ico">
</head>
<body>
    <app-root>Loading...</app-root>
</body>
</html>
```

Body etiketinin içinde html standardına uymayan özel bir etiketimiz var, `app-root` elementi.

Eğer `app` klasörüne göz atarsanız ve `app.component.ts` adlı dosyayı açarsanız aşağıdaki gibi olduğunu göreceksiniz.

```ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css']
})
export class AppComponent {
}
```

Gördüğünüz gibi 'selector' olarak 'app-root' seçilmiş. Angular komponentleri elementlere `selector` adı verilen seçiciler ile bağlanırlar. Seçiciler bir bir çeşit css element seçicisi gibidir. Eğer `name` yazarsanız bir `etiket` seçmiş olursunuz, `.name` yazarsanız bir `class` seçmiş olursunuz ya da `[name]` yazarsanız bir `property` seçmiş olursunuz.

`templateUrl` özelliği komponentin arayüz şablonunun konumunu tutar. Bunun yerine `template` özelliğini kullanarak direkt bu dosyaya da html şablon yazabilirsiniz, ihtiyacınıza göre buna siz karar verebilirsiniz.

```ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  template: `
    <b>hi</b>
  `,
  styleUrls: ['./app.component.css']
})
export class AppComponent {
}
```

`styleUrls` özelliği bize komponentin stil dosyasının konumunu gösterir. Yine yukarıda olduğu gibi `styles` kullanarak da css dosyası kullanmadan direkt olarak bu dosyaya css yazabilirsiniz. Ancak `template` ile `styles` arasında bir fark bulunur, styles bir string dizisi kabul eder, doğrudan string veremezsiniz.

```ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  template: `
    <b>hi</b>
  `,
  styles: [
      `b {
          color: red;
      }`
  ]
})
export class AppComponent {
}
```

`app.component.spec.ts` dosyası testler hakkında işlemler içerir. Şimdilik bunu da erteliyoruz. (Söylemiştim testlerin kaderi bu.)

Angular projeleri modüller ile çalışır. Bu moduller `java` daki paketlere ya da `c#` daki isim uzaylarına benzerler. Sizin komponentleriniz bir modulde tanımlanır. `app.module.ts` dosyası ana modulu içerir.


```ts
import { BrowserModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';
import { FormsModule } from '@angular/forms';
import { HttpModule } from '@angular/http';

import { AppComponent } from './app.component';

@NgModule({
  declarations: [
    AppComponent
  ],
  imports: [
    BrowserModule,
    FormsModule,
    HttpModule
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }
```

Projede kullanılacak tüm komponentler bu dosyada deklare edilmelidir. Eğer burada deklare etmezsek kullandığımız zaman angular bu komponentleri bulamaz.

Şu anda diğer dosyaları ayrıntılı olarak açıklamak istemiyorum. Bunlara da sonra geleceğiz.

> Daha derine gitmeden önce typescript öğrenmenizi tavsiye ediyorum. Eğer konu hakkında bilginiz yoksa bi göz atıp sonra buradan devam edin.


### Yeni bir komponent oluşturmak

Yeni bir komponent oluştururken; önce `./src/app` dizininde bir `server` adında bir klasör oluşturalım.
Bu klasör içinde de `server.component.ts` adında bir dosya oluşturalım. Ayrıca `server.component.html` adında bir dosya daha oluşturmalısınız.

server.component.ts içinde;

```ts
export class ServerComponent {

}
```

`ServerComponent` adında bir sınıf oluşturduk ve sınıfı export ettik. Eğer export etmeseydik bu sınıfı dışarıda kullanamazdık. Hala yapmamız gereken işler var. Bu sınıfı bir komponente çevirecek bir `decorator` oluşturmalıyız. Hadi yapalım o zaman?

```ts
@Component({

})
export class ServerComponent {

}
```

Bu şekilde derlenmeyecektir. Bir şey daha dahil etmeliyiz. `Component` dekoratörü `@angular/core` paketi içinde tanımlı. Bu paketi şu şekilde import edebiliriz.

```ts
import { Component } from '@angular/core';

@Component({

})
export class ServerComponent {

}
```
Artık anguların kullanabileceği bir komponent oluşturmuş durumdayız. Fakat hala geçersiz. Çünkü bir `selector`'e sahip değil. Var olmasına rağmen herhangi bir yerde çağırılmış değil. Bu yüzden ona bir `selector` deklare etmeliyiz.

```ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-server'
})
export class ServerComponent {

}
```

`selector` css seçicisi gibidir. Herhangi bir yere direkt olarak `app-server` yazarsanız; `<app-server></app-server>` şeklinde görünecektir. Eğer `.app-server` şeklinde kullanırsanız `<div class="app-server"></div>`. Hatta `[app-server]` bir özellik(property, attribute) olarak bile kullanabilirsiniz. (şöyle `<div app-server></div>`).

Komponentin html dosyasını komponente bağlamalıyız. Bunun için `templateUrl` kullanacağız. Tıpkı `app.component` içinde olduğu gibi.

```ts
import {Component} from '@angular/core';

@Component({
  selector: 'app-server',
  templateUrl: './server.component.html'
})
export class ServerComponent {

}
```

Bu komponenti kullanabilmek için `app.module.ts` içinde deklare etmeliyiz.


```ts
import { BrowserModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';
import { FormsModule } from '@angular/forms';
import { HttpModule } from '@angular/http';

import { AppComponent } from './app.component';
import { ServerComponent } from './server/server.component' // <<-- önce buradan import ediyoruz

@NgModule({
  declarations: [
    AppComponent,
    ServerComponent // <<-- ardından burada deklarasyonumuza ekliyoruz
  ],
  imports: [
    BrowserModule,
    FormsModule,
    HttpModule
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }

```

Şimdi `server.component.html` dosyasını değiştireceğim.

```html
<b> server component </b>
```

Artık bu komponenti kullanbiliriz. Hemen `app.component.html` içinde kullanalım.

```html
<b> app component </b>

<app-server></app-server>
```

Şimdi [http://localhost:8080](http://localhost:8080) adresine bir göz atalım.

![](images/1.png)

### Komut satırı ile bir komponent oluşturmak

Bazen sürekli kendini tekrar eden yapıları üst üste oluşturmak istemeyebiliriz. Bu durum için `@angular/cli`'in bir çözümü var. `ng` nin generate fonksiyonu bize yeni komponentler oluşturmak için yardımcı oluyor.

```
ng generate component <name>
or
ng g c <name>
```

Eğer bir servers adında bir komponent oluşturmak istersek.

```
ng generate component servers
```

`app` dizini içine `servers` klasörü oluşturacak, onun da içine `ts`i `html`, `css` ve `.spec.ts` dosyalarını otomatik oluşturacaktır. Ayrıca `app.module.ts` içine bizim yerimize deklarasyon ekleyecek kısaca komponenti direkt olarak kullanıma hazır hale getirecektir.


### Projeye bootstrap css eklemek

Projemizde Boostrap'e ihtiyaç duyabiliriz. Nasıl import edeceğiz? İlk olarak indirmek zorundayız.

```
npm install bootstrap --save
```

Ardından `.angular-cli.json` dosyasını açarak şu şekilde düzenlemeliyiz.

```js
{
  "$schema": "./node_modules/@angular/cli/lib/config/schema.json",
  "project": {
    "version": "1.0.0-beta.32.3",
    "name": "new-cli"
  },
  "apps": [
    {
      "root": "src",
      "outDir": "dist",
      "assets": [
        "assets",
        "favicon.ico"
      ],
      "index": "index.html",
      "main": "main.ts",
      "polyfills": "polyfills.ts",
      "test": "test.ts",
      "tsconfig": "tsconfig.json",
      "prefix": "app",
      "styles": [
        "../node_modules/bootstrap/dist/css/bootstrap.min.css", // <<-- bu satırı ekledik
        "styles.css"
      ],
      "scripts": [],
      "environmentSource": "environments/environment.ts",
      "environments": {
        "dev": "environments/environment.ts",
        "prod": "environments/environment.prod.ts"
      }
    }
  ],
  "e2e": {
    "protractor": {
      "config": "./protractor.conf.js"
    }
  },
  "lint": [
    {
      "files": "src/**/*.ts",
      "project": "src/tsconfig.json"
    },
    {
      "files": "e2e/**/*.ts",
      "project": "e2e/tsconfig.json"
    }
  ],
  "test": {
    "karma": {
      "config": "./karma.conf.js"
    }
  },
  "defaults": {
    "styleExt": "css",
    "component": {}
  }
}

```

Artık bootstrap kullanıma hazır.

>**Note:** Bootstrap için bir kütüphane mevcut [bootstrap](https://github.com/ng-bootstrap/ng-bootstrap). Kolayca kullanabileceğimiz bir çok komponent içeriyor.


### Databinding

Databinding basitçe şablonlar ve sınıflar arasında verilerin bağlanmasını sağlar.

* **OUT** String Interpolation: Değişkeni şablona bağlar. Yazımı `{{ data }}` şeklindedir.
* **OUT** Property Binding: Bir değişkeni şablonun bir özelliğine atar. Yazımı `[property]="data"` şeklindedir.
* **IN** Olay yakalama: Olayı sınıftaki bir methoda bağlama. Yazımı `(event)="expression"` şeklindedir.

#### String Interpolation

Hadi isim yazan basit bir komponent yaratalım. İsim String Interpolation ile bizim sınıfımız içinde tanımlansın.  

```ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-name',
  template: `
    <p> My name is {{name}} </p>
  `
})
export class NameComponent {
  name: string = "Doğan";
}
```

Sonuç:

![](images/2.png)


Bu sefer 1 saniyelik bir gecikme ekleyelim. 1 saniyenin ardından ismin Göksel olarak değişeceğini göreceğiz. Ne kadar güzel bir isim.

```ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-name',
  template: `
    <p> My name is {{name}} </p>
  `
})
export class NameComponent {
  name: string = "Doğan";

  constructor() {
    setTimeout(() => {
      this.name = "Göksel";
    }, 1000);
  }
}
```

Başlangıçta bize ` My name is Doğan ` yazmasının 1 saniye sonrasında ` My name is Göksel ` yazısını gördük. Databinding şablonu render etti. Yani render konusunu kafanıza takmayın.

#### Property binding and Event Binding

Şimdi diğer databinding(veri bağlama) tiplerini de görelim.

```ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-name',
  template: `
    <button [disabled]="isDisabled" (click)="someAction()">Regular button</button>
    <button (click)="changeDisabled()"> {{isDisabled}} </button>
  `
})
export class NameComponent {
  isDisabled = true;

  someAction() {
    alert("hello");
  }

  changeDisabled() {
    this.isDisabled = !this.isDisabled; // değeri ters çevir
  }
}
```

Başlangıçta button tıklanamaz durumda. Ancak diğer butona tıkladığımızda artık tıklanabilir duruma geçiyor ve siz butona tıkladığınızda "merhaba" diyen bir alert görüyorsunuz.

#### Two way databinding

Angular'da bir databinding tipi daha var. Bu da `Two way databinding` (İki yönlü veri bağlama). Bu sefer olaylar, özellikler ve sınıflar bağlanacak.

```ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-name',
  template: `
    <input [(ngModel)]="name"> 
    
    <p> My name is {{name}} </p>
  `
})
export class NameComponent {
  name: string = "Doğan";
}
```

Göreceksiniz input içindeki name özelliği değiştiğinde ` My name is _____ ` kısmı da otomatik olarak yeniden render edilecek. Eğer sınıftaki name özelliğini değiştirirseniz de input içindeki değer değişecektir.

> **Note:** `ngModel` `app.module.ts` dosyasında import edilmek zorundadır. Gerekli modülün adı `FormsModule`.

### Direktifler

3 tip direktif var.

* Komponentler
* Yapısal Direktifler (bunları `*` yıldız karakteri olarak göreceksiniz) 
* Özellik Direktifleri

Komponentleri artık zaten biliyorsunuz. Hadi yapısal direktiflere geçelim.

Bu direktifler dom'un tamamını kontrol ederler. Neden diye sorabilirsiniz.

#### ngIf

Hadi `*ngIf` örneğine bir göz atalım


```ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-name',
  template: `
    <button (click)="visible = !visible">{{visible}}</button>
    <p *ngIf="visible">
      I'm visible now
    </p>
  `
})
export class NameComponent {
  visible: boolean = false;
}
```

Bu örnekte biz butona tıkladığımızda bir metin beliriyor. Ancak ilginç olan visible değişkeni false olduğunda p elementi henüz yok. Sadece visible değeri true olduğunda yaratılıyor. Yapısal direktifler var olan domu düzenler ya da yok ederler.

Ayrıca else de (Angular 4) kullanabilirsiniz.


```ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-name',
  template: `
    <button (click)="visible = !visible">{{visible}}</button>
    <p *ngIf="visible; else hidden">
      I'm visible now
    </p>
    <ng-template #hidden>
      <p>
        I'm hidden
      </p>
    </ng-template>

  `
})
export class NameComponent {
  visible: boolean = false;
}
```

Devam etmeden önce lütfen deneyin.

#### ngFor

ngFor da yapısal bir direktifdir. Verilen diziye göre kendini düzenler ve kopyalar. Örneğin;

```ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-name',
  template: `
    <ul>
      <li *ngFor="let car of cars">{{car}}</li>
    </ul>
  `
})
export class NameComponent {
  cars = [
    'Toyota',
    'Honda',
    'Ford'
  ]
}
```

![](images/3.png)

ngFor ayrıca index'e de sahiptir. Eğer `;` bu kapsamda kullanabileceğiniz bir index değişkeni tanımlayabilirsiniz.

```ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-name',
  template: `
    <ul>
      <li *ngFor="let car of cars; let i = index">({{i}}) {{car}}</li>
    </ul>
  `
})
export class NameComponent {
  cars = [
    'Toyota',
    'Honda',
    'Ford'
  ]
}
```

![](images/4.png)


#### ngStyle

ngStyle bir özellik direktifidir. Yapısal direktifler gibi görünmez.

```ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-name',
  template: `
    <ul>
      <li *ngFor="let car of cars" [ngStyle]="{backgroundColor: car.total > 0 ? 'green' : 'red'}">{{car.name}}</li>
    </ul>
  `
})
export class NameComponent {
  cars = [
    {
      name: 'Toyota',
      total: 1
    },
    {
      name: 'Ford',
      total: 0
    }
  ]
}
```

Toyota elemanının yeşil Ford elemanının kırmızı olduğunu göreceksiniz.

#### ngClass

ngClass da özellik direktifidir.

```ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-name',
  template: `
    <ul>
      <li *ngFor="let car of cars" [ngClass]="{notInStock: car.total == 0}">{{car.name}}</li>
    </ul>
  `,

  styles: [
    `.notInStock {
      background-color: red
    }`
  ]
})
export class NameComponent {
  cars = [
    {
      name: 'Toyota',
      total: 1
    },
    {
      name: 'Ford',
      total: 0
    },
  ]
}
```

Toyota elemanının normal ancak Ford elemanının kırmızı göründüğünü göreceksiniz.

#### ngSwitch

ngSwitch is for switching between multiple cases. Its very usefull built-in directive.

```ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-name',
  template: `
    <div [ngSwitch]="count">
      <p *ngSwitchCase="5"> Count is 5 </p>
      <p *ngSwitchCase="10"> Count is 10 </p>
      <p *ngSwitchDefault> Count is Default </p>
    </div>
  `
})
export class NameComponent {
  count: number = 5;
}
```


### Input

In this chapter our goal is making some property to accessible from outside. You may ask why we need this? We creating components that has own scope. For example we create "create new user" component and  "user list" component. So one component must effect to another one. 

First lets do what we wanted. We will create some components.

```bash
ng new my-second-app
cd my-second-app
ng g c users --spec false    #-- spec false blocks spec file generation
ng g c users/user-list --spec false # users/list syntax will create a component in users folder. 
ng g c users/user-item --spec false
ng g c users/user-create --spec false
```

Edit app.component.html as this

```html
<app-users></app-users>
```


Edit users.component.html as this

```html
<app-user-create></app-user-create>
<hr>
<app-user-list></app-user-list>
```

Add an array to user-list component file.

```ts
import { Component, OnInit } from '@angular/core';

@Component({
  selector: 'app-user-list',
  templateUrl: './user-list.component.html',
  styleUrls: ['./user-list.component.css']
})
export class UserListComponent implements OnInit {
  users = ['Jack', 'George', 'Another common name']; // << this line
  
  constructor() { }

  ngOnInit() {
  }
}
```

Edit user-list.component.html as this

```html
<app-user-item *ngFor="let user of users"></app-user-item>
```

Edit user-item.component.html and user-item.component.ts as like this.

```html
<p>
  User name: {{name}} 
  <button>Edit</button>
  <button>Delete</button>
</p>
```

```ts
import { Component, OnInit } from '@angular/core';

@Component({
  selector: 'app-user-item',
  templateUrl: './user-item.component.html',
  styleUrls: ['./user-item.component.css']
})
export class UserItemComponent implements OnInit {
  name: string;
  constructor() { }

  ngOnInit() {
  }

}
```

So now we ready to process. If you get this point you probably see this screen.

![](images/5.png)

User fields are created but name seems doesn't work at all. We have to do something don't we. UserItemComponent element's name property cannot be accessed by other component because it works in own closure. We have to add a decorator to access. Its called `@Input`

We now editing user.component.ts 


```ts
import { Component, OnInit } from '@angular/core';

@Component({
  selector: 'app-user-item',
  templateUrl: './user-item.component.html',
  styleUrls: ['./user-item.component.css']
})
export class UserItemComponent implements OnInit {
  @Input() name: string;
  constructor() { }

  ngOnInit() {
  }

}
```

`@Input` decorator is actually decorator generating function. So we have to call it like `@Input()`. You can use the first parameter as alias. I will give you an example for it too.

Now we test our application but result is same. Nothing changed :worried:

![](images/5.png)

We forgot to set name because we never set it or access it from outside of user-item component. 

Edit the user-list.component.html

```html
<app-user-item *ngFor="let user of users" [name]="user"></app-user-item>
```

As you can see, we used a property binding. Basically `@Input` working as property. We set the value as user, because we declared a variable as `user` in ngFor directive.

Now give a shot. 

![](images/6.png)

Lets check example of the alias parameter `@Input()`. 

app-user-item.ts

```ts
import { Component, OnInit } from '@angular/core';

@Component({
  selector: 'app-user-item',
  templateUrl: './user-item.component.html',
  styleUrls: ['./user-item.component.css']
})
export class UserItemComponent implements OnInit {
  @Input('user') name: string; // << as you can see we give some parameter 
  constructor() { }

  ngOnInit() {
  }

}
```

Now component looking for `user` property. 


Edit the user-list.component.html

```html
<app-user-item *ngFor="let user of users" [user]="user"></app-user-item>
```

### Output

Last chapter we dive into Input. In our example we created edit and delete buttons. Also we must have a working user-create component too. Lets check it.

user-create.component.html

```html
name: <input type="text" [(ngModel)]="name">
<button (click)="onUserCreate()">create</button>
```

user-create.component.ts

```ts
import { Component, OnInit, Output, EventEmitter } from '@angular/core';

@Component({
  selector: 'app-user-create',
  templateUrl: './user-create.component.html',
  styleUrls: ['./user-create.component.css']
})
export class UserCreateComponent implements OnInit {

  constructor() { }

  ngOnInit() {
  }

  name: string; // two-way-binding property

  @Output()
  onUserCreated = new EventEmitter<string>(); // this is the our event that can be binded out of this component
  // note: EventEmitter should be imported from @angular/core

  onUserCreate() { // this function get trigger when user click button
    this.onUserCreated.emit(this.name);  // we send data to eventemitter
  }
}
```

> **Note:** I will move users to upper component.

users.component.html

```html
<app-user-create (onUserCreated)="onUserCreated($event)"></app-user-create>
<hr>
<app-user-list [users]="users"></app-user-list>
```

users.component.ts

```ts
import { Component, OnInit } from '@angular/core';

@Component({
  selector: 'app-users',
  templateUrl: './users.component.html',
  styleUrls: ['./users.component.css']
})
export class UsersComponent implements OnInit {
  users = ['Jack', 'George', 'Another common name'];

  constructor() { }

  ngOnInit() {
  }

  onUserCreated(name) {
    this.users.push(name);
  }
}
```

user-list.component.ts

```ts
import { Component, OnInit, Input } from '@angular/core';

@Component({
  selector: 'app-user-list',
  templateUrl: './user-list.component.html',
  styleUrls: ['./user-list.component.css']
})
export class UserListComponent implements OnInit {
  @Input() // added this
  users; 
  
  constructor() { }

  ngOnInit() {
  }

}
```

Lets check our application. We type some name to input. Then click the create button. :sunglasses:

### View Encapsulation

Component's css files are specific to component. For example in css file;

```css
b {
  color: red;
}
```

This css compiled with some property selector so this way other components b element won't get any effect but you may don't want to do that. Simply changing encapsulation can modify this feature.

```ts
import { Component, ViewEncapsulation } from '@angular/core';

@Component({
  selector: 'app-some',
  templateUrl: './some.component.html',
  styleUrls: ['./some.component.css'],
  encapsulation: ViewEncapsulation.None
})
export class SomeComponent {

}
```

### Local reference

Local reference makes a marking for DOM elements. We use that in `*ngIf` structure directive section. There is one more thing that I should write and thats named `@ViewChild` decorator.

This decorator allows to access DOM element from code. If you know what are you going to do then you can use this decorator, otherwise please avoid using this feature.

```ts
import { Component, ViewChild, ElementRef } from '@angular/core';

@Component({
  selector: 'app-some',
  template: `
  <div #localReference>

  </div>
  `
})
export class SomeComponent {
  @ViewChild('localReference') 
  localReferenceDiv: ElementRef;
}
```


### ng-content

ng-content is a special directive that provide element's content. Normally angular will override the content of components. `<app-root>Loading...</app-root>` is good example for this consept. When angular handle `app-root` then `Loading` text will disapear. But what if we want it. 

Let me show you an example.

```ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-bold',
  template: `
    <b>
      <ng-content></ng-content> <!-- all content will goes to this -->
    </b>
  `
})
export class BoldComponent {
}
```

```ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  template: `
    <app-bold> this text will be bold </app-bold>
  `
})
export class AppComponent {
}
```

> **Note:** Last chapter we learnt ViewChild. If you want to use ViewChild in a content it won't work. You have to use `@ContentChild`

### Life cycle of components

Components have a standard life cycle. They all have these things. We can hook them.

* ngOnChanges: Called after a bound input proerty changes
* ngOnInit: Called once the component initalized
* ngDoCheck: Called during every change detection run
* ngAfterContentInit: Called after content (ng-content) has been projected into view
* ngAfterContentChecked: Called every time the projected content has been checked
* ngAfterViewInit: Called after the component's view (and child views) has been initalized.
* ngAfterViewChecked: Called every time the view (and child views) has been checked.
* ngOnDestroy: Called once the components is about the be destroyed.

```ts
import { Component, OnInit, OnChanges, SimpleChanges, DoCheck, AfterContentInit, AfterContentChecked, AfterViewInit, AfterViewChecked, OnDestroy } from '@angular/core';

@Component({
  selector: 'app-some',
  template: ` `
})
export class SomeComponent implements OnInit, OnChanges, DoCheck, AfterContentInit, AfterContentChecked, AfterViewInit, AfterViewChecked, OnDestroy {

    ngOnChanges(changes: SimpleChanges): void {
    console.log('ngOnChanges', changes);
  }

  ngOnInit(): void {
    console.log('ngOnInit');
  }

  ngDoCheck(): void {
    console.log('ngDoCheck');
  }

  ngAfterContentInit(): void {
    console.log('ngAfterContentInit');
  }

  ngAfterContentChecked(): void {
    console.log('ngAfterContentChecked');
  }

  ngAfterViewChecked(): void {
    console.log('ngAfterViewChecked');
  }

  ngAfterViewInit(): void {
    console.log('ngAfterViewInit');
  }

  ngOnDestroy(): void {
    console.log('ngOnDestroy');
  }
}
```


### Creating a new directive

We saw some already defined directives. But how we can defire new? This chapter we will dive into that.

Directives are defining just like components. You have to add them to app.module.ts. We can create manual but I will use @angular/cli.

```
ng generate directive <name>
or
ng g d <name>
```

I will create a green directive that makes elements green on hover.

```
ng g d green
```

I remove spec.ts file because we don't care tests just now. There should be green.directive.ts file. Directive files are created as `<name>.directive.ts` syntax. 

```ts
import { Directive } from '@angular/core';

@Directive({
  selector: '[appGreen]'
})
export class GreenDirective {
  constructor() { }
}
```

This directive will handle the `appGreen` property. If you use somewhere else this then directive will bound to element.

#### HostListener

We trying to make green element whenever mouse hover's the element so we have to catch the events.

```ts
import { Directive, HostListener } from '@angular/core';

@Directive({
  selector: '[appGreen]'
})
export class GreenDirective {
  constructor() { }

  @HostListener('mouseenter')
  mouseenter() {
    // mouse enters
  }

  @HostListener('mouseleave')
  mouseleave() {
    // mouse leaves
  }
}
```

#### HostBinding

How about to change colors? Now we use `@HostBinding`.

```ts
import { Directive, HostBinding, HostListener } from '@angular/core';

@Directive({
  selector: '[appGreen]'
})
export class GreenDirective {
  @HostBinding('style.backgroundColor') backgroundColor: string = 'transparent';

  @HostListener('mouseenter')
  mouseenter() {
    this.backgroundColor = 'green';
  }

  @HostListener('mouseleave')
  mouseleave() {
    this.backgroundColor = 'transparent';
  }
}
```

### Services and dependency injection

Services useful to carry data between components. We do not require any decorator to create service. Lets create an user service.

I recommend to create file as `<name>.service.ts` syntax. 

So lets create a new users.service.ts file on `app` folder.

```ts
export class UserService {
  users = [
    {id: 1, name: 'co3moz'},
    {id: 2, name: 'goxel'}
    {id: 3, name: 'Ilrkhoaktul'}
  ]

  getUsers() {
    return this.users;
  }

  addUser(user: {id: number, name: string}) {
    this.users.push(user);
  }

  removeUser(id: number) {
    this.users.splice(id, 1);
  }
}
```

We basically create an users service class with some property and functions.

Lets use it from a component.

```ts
import { UserService } from 'user.service';
import { Component } from '@angular/core';

@Component({
  selector: 'app-user-list',
  template: `
    <p *ngFor="let user of users"> {{ user.name }} </p>
  `,
  providers: [
    UserService
  ]
})
export class UserListComponent implements OnInit {
  users;
  constructor(private userService: UserService) {} // userService's type must be declared. Otherwise it won't work.

  ngOnInit() {
    this.users = this.userService.getUsers(); // pass reference of array to local variable.
  }
}
```

> **Important Note:** Providers will provide a service to component but every creation of userlistComponent will make own UserService. Because we said to component when you initializing create a new service that called UserService. But what if we just want to application wide? We may need to use this datas from outside of this component. We have to use app.module.ts file for this job. Inside of app.module.ts there is providers section that we can put our service. 

> **Important Note 2:** Children of userListComponent can access same service if they didn't declared a new provider of UserService. So Providers section of component should be used only for creating new provider.

You can use `@angular/cli` to generate service

```
ng generate service <name>
or
ng g s <name>
```

#### Injecting a service into another service

We may need a service inside of another service. For example we may have a logging service and this service may required to other places. So how we use another service in our service?

There you go, some example of `@Injectable`

```ts
import { LoggingService } from 'logging.service';
import { Injectable } from '@angular/core';

@Injectable()
export class UserService {
  users = [
    {id: 1, name: 'co3moz'},
    {id: 2, name: 'goxel'}
    {id: 3, name: 'Ilrkhoaktul'}
  ];

  constructor(private loggingService: LoggingService) {

  }

  getUsers() {
    return this.users;
  }

  addUser(user: {id: number, name: string}) {
    this.users.push(user);
    this.loggingService.log('user added');
  }

  removeUser(id: number) {
    this.users.splice(id, 1);
    this.loggingService.log('user removed');
  }
}
```


#### Event emitting service

We may need a event that emits some information.

```ts
import { LoggingService } from 'logging.service';
import { Injectable, EventEmitter } from '@angular/core';

@Injectable()
export class UserService {
  users = [
    {id: 1, name: 'co3moz'},
    {id: 2, name: 'goxel'}
    {id: 3, name: 'Ilrkhoaktul'}
  ];

  constructor(private loggingService: LoggingService) {

  }

  userCreated = new EventEmitter<{id: number, name: string}>();

  getUsers() {
    return this.users;
  }

  addUser(user: {id: number, name: string}) {
    this.users.push(user);
    this.userCreated.emit(user);
    this.loggingService.log('user added');
  }

  removeUser(id: number) {
    this.users.splice(id, 1);
    this.loggingService.log('user removed');
  }
}
```

In component we can just subscribe the event. We will learn better feature so this feature is just for knowledge.

```ts
import { UserService } from 'user.service';
import { Component } from '@angular/core';

@Component({
  selector: 'app-user-list',
  template: `
    <p *ngFor="let user of users"> {{ user.name }} </p>
  `,
  providers: [
    UserService
  ]
})
export class UserListComponent implements OnInit {
  users;
  constructor(private userService: UserService) {
    this.userService.userCreated.subscribe((user) => {
      console.log('new user just created');
    });
  } // userService's type must be declared. Otherwise it won't work.

  ngOnInit() {
    this.users = this.userService.getUsers(); // pass reference of array to local variable.
  }
}
```

> **Important Note:** When you subscribing manually don't forget to unsubscribe with `ngOnDestroy`.


### Router

Router is routes components as pages. To you router first go `app.module.ts`

Import the Routes from `@angular/router`

```ts
import { Routes, RouterModule } from '@angular/router';
```

Then create a array that contains following objects.

```ts
const appRoutes: Routes = [
  { path: 'users', component: UsersComponent}
];
```

`path` declares a route in browser. for example `users` makes routes for `/users`. If path given as empty string then it routes for ` ` so this means we can make a home page.

```ts
const appRoutes: Routes = [
  { path: '', component: HomeComponent},
  { path: 'users', component: UsersComponent}
];
```

Also you must add `RouterModule.forRoot(appRoutes)` to imports section of `AppModule`.

> **Note** You may create a `app.route.ts` or `app.routing.ts` file. Its your decision.

Now we have to declare where will content go? we will use `<router-outlet></router-outlet>`.

I will add this to app.component.html.

#### Links

In this sub-chapter we will learn router links. 

Normally to make link we simple use `href`.

```html
<a href="/home">Home</a>
```

But for angular its invalid because every click causes full page reload. Our application must be stable as possible as can. 

We will use `routerLink` directive.

```html
<a routerLink="/home">Home</a>
```

You may use `[]` syntax for expressions.

```html
<a [routerLink]="['/user', id]">Home</a>
```

#### Active route

We may need to style active page or etc. To archive this we will use `routerLinkActive`.

```html
<div routerLinkActive="active">
  <a routerLink="/">Home</a>
</div>
```

routerLinkActive directive has a another directive that named `routerLinkActiveOptions`. With routerLinkActiveOptions we can give options to routerLinkActive. For example for full path check;

```html
<div routerLinkActive="active" [routerLinkActiveOptions]="{exact: true}">
  <a routerLink="/">Home</a>
</div>
```

#### Navigating from code

Accesing the router from a component might be useful sometimes.

```ts
import { Component } from '@angular/core';
import { Router } from '@angular/router';

@Component({
  selector: 'app-user-list',
  template: ``
})
export class UserListComponent  {
  constructor(private router: Router) {
  } 

  navigateSomewhereElse() {
    this.router.navigate(['/home']);
  }

}
```


#### Parameters of routes

Examples can show everything.

```ts
const appRoutes: Routes = [
  { path: '', component: HomeComponent},
  { path: 'users/:id', component: UsersComponent}
];
```

```ts
import { Component } from '@angular/core';
import { ActivatedRoute } from '@angular/router';

@Component({
  selector: 'app-user-list',
  template: ``
})
export class UsersComponent  {
  constructor(private route: ActivatedRoute) {
  } 

  getIdParameter() {
    return this.route.snapshot.params['id'];
  }

}
```

#### Nested routes

Nested routes are useful when we need show multiple components at same time.

```ts
const appRoutes: Routes = [
  { path: '', component: HomeComponent },
  { path: 'users', component: UsersComponent, children: [
    { path: ':id', component: UserComponent },
    { path: ':id/edit', component: UserEditComponent }
  ]}
];
```

Don't forget to add `<router-outlet></router-outlet>` to parent component.


#### Redirecting

We may need a redirecting route. I achive that we simple add a route which doesn't have component property. It needs only `redirectTo` parameter.

```ts
const appRoutes: Routes = [
  { path: '', component: HomeComponent },
  { path: 'users', component: UsersComponent },
  { path: 'people', redirectTo: '/users' }
];
```

With this feature and wildcard feature we can make 404 pages.


```ts
const appRoutes: Routes = [
  { path: '', component: HomeComponent },
  { path: 'users', component: UsersComponent },
  { path: 'not-found', component: NotFoundComponent },
  { path: '**', redirectTo: '/not-found' } // make sure wildcard is at the end.
];
```

Simply other routes will redirected to `NotFoundComponent`
