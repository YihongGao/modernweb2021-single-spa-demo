# Modernweb 2021 - Single-spa

This is a simple Single-spa example

## Overview
  - root-config (single-spa root-config)  
    1. It is a entry point in web 
    2. Register you **single-spa applications**
    3. Control **single-spa applications** display or not by router

  - navber-app (single-spa application)
    1. It is a simply navbar application with angular

  - vue-app (single-spa application)
    1. It is a vue (version 3) application

## Quick start

 1. Run root-conig 
 ```
    cd root-config
    npm install
    npm run start
 ```

 2. Run navbar-app
 ```
    cd navbar-app
    npm install
    npm run serve:single-spa:navbar-app
 ```

 3. Run vue-app
 ```
    cd vue-app
    npm install
    npm run serve
 ```