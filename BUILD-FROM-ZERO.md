# Modernweb 2021 - Single-spa build from zero

## My Environment
  1. nodeJs - 15.14.0
  2. npm - 7.7.6
  3. angular cli - 12.2.3

## Step
  1. 建立 **root-config** (Single-spa root-config)
  ```
  # 使用 create-single-spa 建立 single-spa 專案
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

  2. 建立 **navbar-app** 並配置為 Single-spa application
  ```
    # 使用 angular-cli 建立 angular 專案
    # 建議 prefix 為唯一值，若 root-config 同時載入兩個 angular application(Single-spa application) 且該 prefix 重複時，則可能會載入錯誤的 application 內容
    # 必需啟用 routing feature
    ng new navbar-app --prefix navbar-app --routing

     # 移動到 navbar-app 目錄
    cd navbar-app

    # 寫入 navbar 的 HTML, CSS
    curl https://raw.githubusercontent.com/YihongGao/modernweb2021-single-spa-demo/master/material/navbar/app.component.html --output ./src/app/app.component.html
    curl https://raw.githubusercontent.com/YihongGao/modernweb2021-single-spa-demo/master/material/navbar/app.component.css --output ./src/app/app.component.css

    # 將 navbar-app 轉為 single-spa application
    ng add single-spa-angular
    /**
      Would you like to proceed? Yes
      ✔ Package successfully installed.
      ? Does your application use Angular routing? Yes
      ? What port should your project run on? 4200
    **/
    npm install

    # 配置 routing
    curl https://raw.githubusercontent.com/YihongGao/modernweb2021-single-spa-demo/master/material/navbar/app-routing.module.ts --output ./src/app/app-routing.module.ts
  ```
  > **重要**: 建議 prefix 為唯一值，若 root-config 同時載入兩個 angular application(Single-spa application) 且該 prefix 重複時，則可能會載入錯誤的 application 內容 

  3. 於 **root-config** 服務中註冊 **navbar-app**  
  ```
  # 移動到 root-config 目錄
  cd ../root-config

  # 將 navbar-app 加入註冊表(ejs) 與 配置 layout-engine(html)
  curl https://raw.githubusercontent.com/YihongGao/modernweb2021-single-spa-demo/master/material/root-config/with-navbar/index.ejs --output ./src/index.ejs
  curl https://raw.githubusercontent.com/YihongGao/modernweb2021-single-spa-demo/master/material/root-config/with-navbar/microfrontend-layout.html --output ./src/microfrontend-layout.html
  ```

  4. 啟動 **root-config** 與 **navbar-app**
  ```
  # 開啟新的 terminal, 並至 root-config 目錄中並啟動服務
  npm run start

  # 開啟新的 terminal, 並至 navbar-app 目錄中並啟動服務
  cd navbar-app
  npm run serve:single-spa:navbar-app
  ```
  > 備註: 現在你能在瀏覽器上使用 [http://localhost:9000] 來檢視目前服務.

  5. 建立 **vue-app** (Single-spa application)
  ```
    # 於專案根目錄使用 create-single-spa 建立 vue project
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

  6. 於 **root-config** 服務中註冊 **vue-app** 
  ```
  # 移動至 root-config
  cd root-config

  # 將 vue-app 加入註冊表(ejs) 與 配置 layout-engine(html)
  curl https://raw.githubusercontent.com/YihongGao/modernweb2021-single-spa-demo/master/material/root-config/finish/index.ejs --output ./src/index.ejs
  curl https://raw.githubusercontent.com/YihongGao/modernweb2021-single-spa-demo/master/material/root-config/finish/microfrontend-layout.html --output ./src/microfrontend-layout.html

  # 移動至 vue 專案並啟動服務
  cd ../vue-app
  npm run serve
  ```

> 備註: 重新整理瀏覽器([http://localhost:9000]) 並可使用功能列表切換， Home 跟 Vue 頁面， 能看到 angualr(navbar-app) 與 vue 同時呈現於畫面上。

[http://localhost:9000]: http://localhost:9000