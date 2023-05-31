# Airflow with WSL 2 
## Possíveis problemas
1) Feature Microsoft-Windows-Subsystem-Linux não esta habilitada, é necessário executar o comando com o powershell em modo administrador.
    ```
    dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
    ```
2) Feature VirtualMachinePlatform não esta habilitada, é necessário executar o comando com o powershell em modo administrador.
    ```
    dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
    ```    



## Preparação do WSL + Ubuntu
1) Instalação do WSL: https://learn.microsoft.com/pt-br/windows/wsl/install
2) Instalação do Ubuntu: com o powershell em modo administrador, executar o comando: 
    ```
    wsl --install -d <Distribution Name>
    ```
    * `<Distribution Name>` é o nome do Ubuntu, ficando ``wsl --install -d Ubuntu``
    * Após executar o comando acima, cadastre um user e pass para logar na máquina e em seguida desligue-o com o comando ```wsl --shutdown``` ou ```exit``` se estiver dentro da máquina.
3) Definir a versão do WSL para o Ubuntu: com o powershell em modo administrador, executar o comando: 
    ```
    wsl --set-version Ubuntu 2
    ```
4) Iniciar novamente a máquina com o comando ``wsl --install -d Ubuntu``
5) Atualizar a máquina com a versão mais recente: ``sudo apt-get update -y && sudo apt-get upgrade -y``
6) Instalação do python 3.9:
    ```
    sudo apt install software-properties-common
    ```
    ```
    sudo add-apt-repository ppa:deadsnakes/ppa
    ```
    ```
    sudo apt install python3.9 -y
    ```
    Verificar se a instalação do python 3.9 foi realizada com sucesso
    ``` 
    python3.9 --version 
    ```
    ```
    sudo apt install python3.9-venv -y
    ```

## Preparação do Airflow no Ubuntu

```bash
# Criar uma pasta e acessa-la
mkdir data-quality && cd data-quality
```

```Python
# Criar ambiente virtual
python3.9 -m venv venv

# Ativar ambiente virtual - Linux
source venv/bin/activate

# Upgrade pip
python3.9 -m pip install --upgrade pip

# Instalação das libs
pip install apache-airflow[amazon,jdbc,celery,virtualenv,google]==2.2.2 -c "https://raw.githubusercontent.com/apache/airflow/constraints-2.2.2/constraints-3.7.txt"
```

```bash
# Iniciar o airflow, será criada uma pasta airflow no Ubuntu
airflow standalone

# Alterar configurações do airflow
sudo vim airflow/airflow.cfg 

# Abrir um outro powershell e digitar somente `wsl`, ir até a pasta em que as dags ficará armazenada na máquina local. A pasta data-quality foi criada na máquina local.
Exemplo: C:\dev\data-quality 

# Digitar `pwd` e copiar o caminho
/mnt/host/c/dev/data-quality

# Voltar para o powershell que foi aberto o arquivo airflow.cfg e realizar as seguintes alterações
dags_folder = /mnt/host/c/dev/data-quality/dags
load_examples = False
default_timezone = America/Sao_paulo
```
