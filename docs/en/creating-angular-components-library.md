# Creating Angular Components Library

> *How to create an Angular 2+ components library, including library project by itself and demo application for visual testing purpose.*

## Boilerplate preparation

First, open a terminal on desired directory and run following commands (variables described below):

```sh
# create a new angular project and switch view into it
ng new '$REPO_NAME' --create-application false
cd '$REPO_NAME'

# generate demo application
ng generate application '$APP_NAME' --prefix '$APP_PREFIX' --style 'scss' --routing false

# generate library project and switch view into it
ng generate library '$LIB_NAME' --prefix '$LIB_PREFIX'
cd '$LIB_NAME'

# make library use SCSS (SASS) styling instead of default CSS
ng config schematics.@schematics/angular:component.styleext scss

# remove example files generated with library
# you can do that manually also
rm 'src/lib/$LIB_NAME.component.ts'
rm 'src/lib/$LIB_NAME.component.spec.ts'
rm 'src/lib/$LIB_NAME.service.ts'
rm 'src/lib/$LIB_NAME.service.spec.ts'
rm 'src/lib/$LIB_NAME.module.ts'

# switch to library path and make a root module
cd '$LIB_NAME/src/lib'
ng generate module '$LIB_NAME' --flat
```

| Variable      | Description                                                                                 |
| ------------- | ------------------------------------------------------------------------------------------- |
| `$REPO_NAME`  | Angular project name, and possibly git repository name too                                  |
| `$APP_NAME`   | Demo application name, possibly should be just a `demo`                                     |
| `$APP_PREFIX` | Demo application components prefix, possibly `demo` too                                     |
| `$LIB_NAME`   | Library name, possibly equal to `$REPO_NAME` or `$REPO_NAME-components` to be more specific |
| `$LIB_PREFIX` | Library components prefix, possibly equal to `$REPO_NAME`                                   |

Open `$LIB_NAME/src/public-api.ts` and make sure that there is only this line:

```typescript
export * from './lib/$LIB_NAME.module';
```

## Adding a test component

Switch back to terminal and generate a test component to ensure it's all work properly:

```sh
ng generate component '$TEST_COMPONENT_NAME'
```

Open `src/lib/$LIB_NAME.module.ts` and make sure that test components is imported as JavaScript module and exported as Angular entity:

```typescript
import { TestComponent } from './test/test.component'; // it's imported here

@NgModule({
  imports: [CommonModule],
  exports: [TestComponent], // and exported here
  declarations: [TestComponent], // don't forget to declare it also!
})
export class LibraryModule {}
```

Open `$LIB_NAME/src/public-api.ts` again and add another line below:

```typescript
export * from './lib/$LIB_NAME.module';
export * from './lib/test/test.component'; // that one
```

## Importing library

Open demo application module at `$APP_NAME/src/app/app.module.ts` and import the library module:

```typescript
import { BrowserModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';

import { AppComponent } from './app.component';
import { LibraryModule } from '$LIB_NAME'; // it's imported here

@NgModule({
  declarations: [AppComponent],
  imports: [
    BrowserModule,
    LibraryModule, // and here
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule {}
```

Imported at demo application library should be built, there are two options for that:

**Option one**, to just build it once and see what's happened. Switch to terminal and enter these commands from project root directory:

```sh
ng build '$LIB_NAME'
ng serve
```

**Option two**, to edit and build it in live. Use these commands:

```sh
# For session 1
ng build '$LIB_NAME' --watch

# For session 2
ng serve
```

Note: these commands must be launched in separate terminal sessions (like in separate windows).

In any way, the result of commands is now available at [localhost:4200](http://localhost:4200/). It's empty for now, because built library is imported, but not used yet.

## Using library

Open `$APP_NAME/src/app/app.component.html`. Remove all of its content and replace it with following:

```html
<$LIB_PREFIX-test></$LIB_PREFIX-test>
```

Where `test` is library test component name. `$LIB_PREFIX-test` is its selector which you can see at `$LIB_NAME/lib/test/test.component.ts` file.

When `app.component.html` will be saved, page at [localhost:4200](http://localhost:4200/) should be refreshed automatically and show some test component contents, it should be `Test component works` text or something similar. Now library and demo are ready for development.
