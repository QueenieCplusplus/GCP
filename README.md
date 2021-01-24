# GCP
移動至此空間

> 前導：https://github.com/QueenieCplusplus/QuickGoThru/blob/master/README.md#cloud-service-vm


科技業冷僻產品如果結合大家知道的現有通俗知識做比喻作敘述，會增進理解，更容易接受他。

  會用雲的兩種客戶：

  一. 正在為網站找家的人，執行環境，因為沒預算買整棟樓宇，所以當租客。
  二. 已經有房子但因為知道時局又識大體的人，從郊外的房換到城市租房，享受更高的交通品質，所以搬家。

  我們就是像是科技的房屋仲介，要為第一種客戶找適合他住的套房、為第二種 （通常他也找好租屋）為他做搬遷 幫她搬遷打包等瑣碎事宜。

  而 GGP 就是世界物業大亨，他擁有全世界各種地段、品質、家具的膠囊套房。

  ＧCE:
       這類似VM 但是內容物如額外怎樣的配置，即房客自己管理、購買~

  GAE:
       好比飯店管理的套房 24小時七天到府服務、配管家、配外送服務～

  Cloud Storage（包含 firebase）:
        好比放 static 資料的倉庫，租倉庫來的（很少需要出入）。

  GKE :
       好比陽明海運或是長榮貨機對各種物品測量、打包和運輸有運籌知識的專家。

> 跟進：

   * IaaS, GCE 虛擬機（遠端部署環境, 可擴展的運算器）
   
      * HA & DR 災難復原和高可用性（備援）

   使用場景:
   (a) data transfer (backup)
   (b) migration (on-premise to Cloud)
   (c) outage 

   Original or Replacement VM:
    無論是虛擬機群組中哪個替代壞掉的原本的虛擬機，都是要一樣的 private IP 設定的，類似電影花木蘭中劉亦菲和替身群組，無論誰替代本尊上陣武打場面，
    流血受傷的，替補的，正式鏡頭前，仍然是一樣的臉孔。
   
   ![vm1](https://raw.githubusercontent.com/QueenieCplusplus/QuickGoThru/master/vm1.png)
     
   ![vm2](https://raw.githubusercontent.com/QueenieCplusplus/QuickGoThru/master/vm2.png)
    
    
   * 雲端記憶體 
   
   應用 1 : https://github.com/QueenieCplusplus/QuickGoThru/blob/master/README.md#db-migration (資料遷移)
   
   應用 2 : https://github.com/QueenieCplusplus/QuickGoThru/blob/master/README.md#cloud-sql-big-data (大數據)

   * SaaS, 應用程式的執行環境 App Engine 實現 Serverless 
   
     https://github.com/QueenieCplusplus/QuickGoThru/blob/master/README.md#serverless
 
   * GCP 網路拓樸 (VPC, GKE)
    
        * System 系統管理： Cloud Consol & Cloud Shell & Cloud Mobile App (可以啟動 200+ API 做流量觀測)
        
        ![cloud console](https://raw.githubusercontent.com/QueenieCplusplus/QuickGoThru/master/cloud%20console.png)
 
        * Network 網路 : Firewall + Coud CDN + DNS + VPC + VPN + IAP
        
           https://github.com/QueenieCplusplus/QuickGoThru/blob/master/README.md#vpc
        
            * VM 建構時會同時設定防火牆
            
                  Allow Http Traffic
        
            * using cloud shell to do remote connection and server deployment
            
            
                  gcloud compute ssh <vm name> --zone <zone>
                  
                  // ssh helps the remote connection in a wrapper of authentication and mapping instance name to IP addr. In this way, it outputes RSA keys pair.
                  
                  generating Public/Private RSA Key Pairs
                  
                  enter PassPhrase (empty for no passphrase)
                  
                  // type Ctrl + C to disconnect the ssh by existing the shell.
                  
                  
            ![vm3](https://raw.githubusercontent.com/QueenieCplusplus/QuickGoThru/master/vm3.png)
                  
                  
             * deploy Nginx Server in SSH'ed VM while ssh connecting
             
                  (1) to get root access
             
                      sudo su-
                   
                  (2) to update OS
                   
                      apt-get update
                      
                  (3) install nginx server
                  
                      apt-get install nginx -y
                      
                      ps auwx | gerp ngix
                      
                  (4) to deploy the VM server
                  
                      click the external IP link of VM instance
                      
                      or
                      
                      add external IP to http://<external IP>/  in browser
                    
 
        * GKE(容器管理工具與 LB 的實現)
        
           https://github.com/QueenieCplusplus/QuickGoThru/blob/master/README.md#gke
      
   * Cloud IAM（Istio Mesh）
   
        * IAM
        
        https://github.com/QueenieCplusplus/QuickGoThru/blob/master/README.md#iap-security
        
            * using cloud shell to do authentication
            
               (request auth credential to make API calls)
            
                  gcloud auth list
                  
                  credential accounts:
                  
                  - <account name>@<domain>.com (active)
                  
                  ctrl + X, Y, enter
            
                  gcloud config list Project (You can list the project ID with this command)
                  
                  [output]
                  project = <project_ID>
        
   * Anthos (Multi-Cloud + GKE)
   
       待續 ...
       
       
       ![anthos](https://miro.medium.com/max/1158/1*qJ1AI-yR2Z_mh9_mrryLQg.gif)
    
   * Cloud SDK (cmd line tool: cloud shell)
   
     (1) check Project ID, organize the cloud resources
   
          export PROJECT_ID = <project id>

          export ZONE = <zone>

          echo $PROJECT_ID

          echo $ZONE

      (2) manage the cloud engine (VM) resorces
      
          gloud compute
          
          gloud compute instances create --help
          
          gcloud compute instances create <vm name> --machine-type <vm ype> --zone <zone> --image <image>
          
      (3) env's help
      
          gcloud config list
      
          gcloud config --help
          
          or
          
          gcloud help config
          
          Enter / Q
          
      (4) check env's components and install it
      
          gcloud components list
          
          sudo apt-get install google-cloud-sdk
          
          gcloud beta interactive
          
          // to enable gcloud interactive mode
          // press tab to complete file path and arg
          // press tab + space bar 
          
          gloud compute instance describe <vm name>
          
          // press F2 to toggle the help on or off
       
       (5) home directory, path and file
       
          (home dir will persist across projects between all cloud shell sessions even VM is terminated or restart.)
       
          cd $Home
          
          vi ./.bashrc
          
          // esc + :wq
      
