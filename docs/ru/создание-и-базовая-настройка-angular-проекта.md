# Создание и базовая настройка Angular-проекта

> *Руководство по подготовке готового проекта на последней версии Angular, с подключением ESLint и Angular Material.*

## Примечение

Актуально на 2021-06 для:

  - Node v14.*
  - NPM v7.*
  - Angular v12.*
  - Angular Material v12.*

## Проверка зависимостей

Перед началом создания проекта удостоверимся, что у нас есть все необходимое:

```sh
# проверяем node.js (14.*)
node --version

# проверяем npm (7.*)
npm --version

# проверяем angular cli (11.*)
ng --version

# 'ng' иногда не работает под windows
# вместо нее можно попробовать ng.cmd
```

Если нет нужной версии Node.js — скачиваем с [nodejs.org](https://nodejs.org/).

Если нет нужной версии Angular CLI — читаем [angular.io/cli](https://angular.io/cli) и устанавливаем все командой в терминале:

```sh
# в любом месте, cli все равно установится глобально
npm install --global @angular/cli
```

## Генерация проекта

В любом удобном месте запускаем команду:

```sh
ng new --routing true --strict false --style 'scss' '<project-name>'
```

Команда создаст новый проект в директории `<project-name>`. Перейдем в директорию и попробуем запустить проект:

```sh
cd '<project-name>'
ng serve
```

Если после этого проект скомпилировался и стал доступен на [localhost:4200](http://localhost:4200/) — то все хорошо. Я рекомендую проверять работоспособность проекта после каждого шага.

## Подключение ESLint

C 12-ой версии ESLint подключается к новому проекту одной командой, которую необходимо выполнить в директории проекта ([источник](https://github.com/angular-eslint/angular-eslint)):

```sh
ng add @angular-eslint/schematics

# ? The package @angular-eslint/schematics@12.1.0 will be installed and executed. Would you like to proceed?
# > Yes
```

## Подключение Angular Material

Удобнее всего разрабатывать приложение с готовыми компонентами интерфейса — в этом может помочь проект [Angular Material](https://material.angular.io/) и его [библиотека компонентов](https://material.angular.io/components/categories).

Установим Angular Material в директории проекта:

```sh
ng add @angular/material

The package @angular/material@12.0.5 will be installed and executed.

# ? Choose a prebuilt theme name, or "custom" for a custom theme:
# > Indigo/Pink

# ? Set up global Angular Material typography styles? (y/N)
# > Yes

# ? Set up browser animations for Angular Material? (Y/n)
# > Yes
```

## Настройка индексного модуля

*Это не самый корректный способ, но в рамках небольших MVP-проектов в этом нет ничего страшного. Более подробно проблема рассмотрена в конце раздела.*

Для того, чтобы компоненты Angular Material были доступны в приложении, необходимо настроить индексный модуль со всеми компонентами.

Сначала создадим SharedModule, он в любом случае понадобится:

```sh
cd src/app
ng generate module shared
```

Внутри директории `shared` создадим файл `material.module.ts` и добавим в него следующее содержимое:

```ts
import {NgModule} from '@angular/core';
import {A11yModule} from '@angular/cdk/a11y';
import {ClipboardModule} from '@angular/cdk/clipboard';
import {DragDropModule} from '@angular/cdk/drag-drop';
import {PortalModule} from '@angular/cdk/portal';
import {ScrollingModule} from '@angular/cdk/scrolling';
import {CdkStepperModule} from '@angular/cdk/stepper';
import {CdkTableModule} from '@angular/cdk/table';
import {CdkTreeModule} from '@angular/cdk/tree';
import {MatAutocompleteModule} from '@angular/material/autocomplete';
import {MatBadgeModule} from '@angular/material/badge';
import {MatBottomSheetModule} from '@angular/material/bottom-sheet';
import {MatButtonModule} from '@angular/material/button';
import {MatButtonToggleModule} from '@angular/material/button-toggle';
import {MatCardModule} from '@angular/material/card';
import {MatCheckboxModule} from '@angular/material/checkbox';
import {MatChipsModule} from '@angular/material/chips';
import {MatStepperModule} from '@angular/material/stepper';
import {MatDatepickerModule} from '@angular/material/datepicker';
import {MatDialogModule} from '@angular/material/dialog';
import {MatDividerModule} from '@angular/material/divider';
import {MatExpansionModule} from '@angular/material/expansion';
import {MatGridListModule} from '@angular/material/grid-list';
import {MatIconModule} from '@angular/material/icon';
import {MatInputModule} from '@angular/material/input';
import {MatListModule} from '@angular/material/list';
import {MatMenuModule} from '@angular/material/menu';
import {MatNativeDateModule, MatRippleModule} from '@angular/material/core';
import {MatPaginatorModule} from '@angular/material/paginator';
import {MatProgressBarModule} from '@angular/material/progress-bar';
import {MatProgressSpinnerModule} from '@angular/material/progress-spinner';
import {MatRadioModule} from '@angular/material/radio';
import {MatSelectModule} from '@angular/material/select';
import {MatSidenavModule} from '@angular/material/sidenav';
import {MatSliderModule} from '@angular/material/slider';
import {MatSlideToggleModule} from '@angular/material/slide-toggle';
import {MatSnackBarModule} from '@angular/material/snack-bar';
import {MatSortModule} from '@angular/material/sort';
import {MatTableModule} from '@angular/material/table';
import {MatTabsModule} from '@angular/material/tabs';
import {MatToolbarModule} from '@angular/material/toolbar';
import {MatTooltipModule} from '@angular/material/tooltip';
import {MatTreeModule} from '@angular/material/tree';
import {OverlayModule} from '@angular/cdk/overlay';

@NgModule({
  exports: [
    A11yModule,
    ClipboardModule,
    CdkStepperModule,
    CdkTableModule,
    CdkTreeModule,
    DragDropModule,
    MatAutocompleteModule,
    MatBadgeModule,
    MatBottomSheetModule,
    MatButtonModule,
    MatButtonToggleModule,
    MatCardModule,
    MatCheckboxModule,
    MatChipsModule,
    MatStepperModule,
    MatDatepickerModule,
    MatDialogModule,
    MatDividerModule,
    MatExpansionModule,
    MatGridListModule,
    MatIconModule,
    MatInputModule,
    MatListModule,
    MatMenuModule,
    MatNativeDateModule,
    MatPaginatorModule,
    MatProgressBarModule,
    MatProgressSpinnerModule,
    MatRadioModule,
    MatRippleModule,
    MatSelectModule,
    MatSidenavModule,
    MatSliderModule,
    MatSlideToggleModule,
    MatSnackBarModule,
    MatSortModule,
    MatTableModule,
    MatTabsModule,
    MatToolbarModule,
    MatTooltipModule,
    MatTreeModule,
    OverlayModule,
    PortalModule,
    ScrollingModule,
  ]
})
export class MaterialModule {}
```

Это индексный файл для всех компонентов из Angular Material. Импортируем его в SharedModule:

```ts
import { NgModule } from '@angular/core';
import { CommonModule } from '@angular/common';

import { MaterialModule } from './material.module'; // <- вот так

@NgModule({
  imports: [
    CommonModule,
    MaterialModule // <- и вот так
  ],
})
export class SharedModule {}
```

### Зачем так делать

Angular Material разбит на множество компонентов, каждый из которых оформлен в своем модуле — например, MatAutocompleteModule содержит в себе компонент-автокомплит и некоторые вспомогательные элементы.

Для того, чтобы в коде приложения мы могли написать вот так —

```html
<p>Крутой автокомплит из Angular Material:</p>
<mat-autocomplete ...>
  <mat-option [value]="...">
    {{ ... }}
  </mat-option>
</mat-autocomplete>
<button>Погнали</button>
```

— нам нужно, чтобы в модуле компонентов, использующим `<mat-autocomplete ...>`, был заимпортирован MatAutocompleteModule:

```ts
import { NgModule } from '@angular/core';
import { CommonModule } from '@angular/common';
import { MatAutocompleteModule } from '@angular/material/autocomplete';

@NgModule({
  imports: [
    CommonModule,
    MatAutocompleteModule // <- вот тут
  ],
})
export class SomeAppModule {}
```

Если же мы используем несколько компонентов из Angular Material, то для **каждого** нужно будет писать такой импорт, а это

  - долго
  - сложно понять, что именно нужно импортировать
  - неочевидно для новичков
  - в тестах тоже нужно — для каждого компонента

### Почему так не нужно делать

Подключать сразу весь индексный модуль — не круто, потому что так при сборке будет импортироваться сразу **весь** Angular Material. В идеале, конечно, лучше подключать все в индивидуальном порядке, но это очень замедлит процесс разработки и тестирования. А потом еще и отладки: компилятор вообще не будет ругаться, если мы используем `<mat-autocomplete ...>` в разметке, но при этом не импортируем его в модуле.

### Почему так можно делать

Как ни крути, а это очень ускоряет процесс разработки, особенно для новичков.

Да, время сборки увеличивается, но только для первого раза (потом все кешируется). Размер бандла также потенциально увеличивается, но, опять же, не настолько значительно.

## Настройка корневого компонента

После подключения нужно настроить корневой компонент, который будет содержать в себе заголовок и боковое меню. Сначала удалим имеющийся AppComponent и все, что с ним связано:

  - `app.component.html`
  - `app.component.scss`
  - `app.component.spec.ts`
  - `app.component.ts`

Затем создадим новый компонент:

```sh
# нужно запускать команду в src, а не в src/app!
ng generate @angular/material:navigation app
```

Немного поправим новый корневой компонент, изменив его селектор:

```ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-root', // <- вот тут было app-app, а надо app-root
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.scss']
})
export class AppComponent {
   // ...
}
```

Готово! Теперь у нас есть стартовый проект на последнем Angular, с настроенным ESLint и Angular Material для создания интерфейса приложения.
