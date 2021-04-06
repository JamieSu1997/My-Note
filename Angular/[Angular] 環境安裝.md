## Angular - 環境安裝

1. #### 線上開發環境

   https://stackblitz.com/

2. #### 本地開發環境

   1. windows IDE =>

      * [Visual Studio Code](https://code.visualstudio.com/) ( 建議安裝以下套件包) 

        * Angular 擴充套件包 :

          * 安裝Angular Extension Pack擴充套件 

            (由於同名的擴充套件好幾套，推薦安裝作者為 **Will 保哥** 的版本)

          * 安裝 [Prettier - Code formatter](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode) 擴充套件

      * [WebStorm](https://www.jetbrains.com/webstorm/) => 需要學生帳號，不然要錢

   

    2. [Node.js](https://nodejs.org/en/) ( 建議安裝 **v12.19.0 LTS** 以上版本)

       安裝完成後，命令提示字元 / Terminal ，輸入以下指令，確認安裝成功。

       ```shell
       > node -v
       確認為 v12.19.0 或以上版本
       
       > npm -v
       確認為 v6.14.8 以上版本
       ```

   3. Angular CLI

      ```shell
      安裝指令
      > npm install -g @angular/cli
      確認安裝，10.1.6以上版本
      > ng version
      ```

3. #### 開始使用 Angular

   1. 建立第一個 Angular 應用

      ```shell
      建立存放project的資料夾(命令提示字元)
      > mkdir MyprojectDir
      
      用剛剛裝的 Angular cli 命令列工具，新建一個 Angular Application 
      > ng new my-first-project
      
      進入建好的 Application 資料夾目錄內
      > cd my-first-projet
      
      執行 Application，也可以使用 npm start
      > ng serve 
      ```

   2. 開啟瀏覽器，輸入網址 http://localhost:4200 

      出現 `XXXXX (剛剛建的 Application 名字) app is running!` ，就代表成功拉 ! !

      ![image](https://user-images.githubusercontent.com/88981/72908193-1c616d80-3d70-11ea-8fbf-01ed33810864.png)

      