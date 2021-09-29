# Modernweb 2021 - Single-spa build from zero

## My Environment
  1. nodeJs - 15.14.0
  2. npm - 7.7.6
  3. angular cli - 12.2.3

## Step
  1. Build **root-config** (Single-spa root-config)
  ```
  # create single-spa 
  npx create-single-spa
  
  /** 
    ? Directory for new project root-config
    ? Select type to generate single-spa root config
    ? Which package manager do you want to use? npm
    ? Will this project use Typescript? No
    ? Would you like to use single-spa Layout Engine Yes
    ? Organization name (can use letters, numbers, dash or underscore) demo
  **/

  ```

  2. Build **navbar-app** (Single-spa application)
  ```
    # create angular app
    ng new navbar-app --prefix navbar-app --routing

    # change app.component.html and app.component.css to navbar content.  

     # go to navbar-app dir.
    cd navbar-app

    # write navbar html and css
    curl https://raw.githubusercontent.com/YihongGao/modernweb2021-single-spa-demo/master/material/navbar/app.component.html --output ./src/app/app.component.html
    curl https://raw.githubusercontent.com/YihongGao/modernweb2021-single-spa-demo/master/material/navbar/app.component.css --output ./src/app/app.component.css

    # add single-spa feature
    ng add single-spa-angular
    /**
      Would you like to proceed? Yes
      ✔ Package successfully installed.
      ? Does your application use Angular routing? Yes
      ? What port should your project run on? 4200
    **/
    npm install

    # configure routes 
    curl https://raw.githubusercontent.com/YihongGao/modernweb2021-single-spa-demo/master/material/navbar/app-routing.module.ts --output ./src/app/app-routing.module.ts
  ```
  > **Important**: argument **prefix** in ng command must be setting different from other single-spa application.  

  3. Register **navbar-app** into **root-config**
  ```
  # go to root-config dir.
  cd ../root-config

  # register application and define layout
  curl https://raw.githubusercontent.com/YihongGao/modernweb2021-single-spa-demo/master/material/root-config/with-navbar/index.ejs --output ./src/index.ejs
  curl https://raw.githubusercontent.com/YihongGao/modernweb2021-single-spa-demo/master/material/root-config/with-navbar/microfrontend-layout.html --output ./src/microfrontend-layout.html
  ```

  4. Run **root-config** and **navbar-app**
  ```
  # go to root-config dir before do run.
  # cd root-config
  npm run start

  # you should be using new terminal
  # go to navbar-app dir before do run.
  cd navbar-app
  npm run serve:single-spa:navbar-app
  ```

  > Note: Now, You can using [http://localhost:9000] show the web page, Can be see the navbar on browser.

  5. Build **vue-app** (Single-spa application)
  ```
    # you should be using new terminal
    # create vue app
    npx create-single-spa
    /**     
      Need to install the following packages:
        create-single-spa
      Ok to proceed? (y) y
      ? Directory for new project vue-app
      ? Select type to generate single-spa application / parcel
      ? Which framework do you want to use? vue
      ? Organization name (can use letters, numbers, dash or underscore) demo

      Vue CLI v4.5.13
      ? Please pick a preset: Default (Vue 3) ([Vue 3] babel, eslint)
    **/
  ```

  6. Register **vue-app** into **root-config** and run it,
  ```
  # go to root-config dir.
  cd root-config

  # register application and define layout
  curl https://raw.githubusercontent.com/YihongGao/modernweb2021-single-spa-demo/master/material/root-config/finish/index.ejs --output ./src/index.ejs
  curl https://raw.githubusercontent.com/YihongGao/modernweb2021-single-spa-demo/master/material/root-config/finish/microfrontend-layout.html --output ./src/microfrontend-layout.html

  # go to vue-app dir and run it.
  cd ../vue-app
  npm run serve
  ```

> Note: Reflash you page ([http://localhost:9000]) and click Vue button on navbar, You can see vue init page in the same URL domain and port.

[http://localhost:9000]: http://localhost:9000