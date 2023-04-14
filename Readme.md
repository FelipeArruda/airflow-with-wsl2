## Airflow with WSL 2

```Python
# Criar ambiente virtual
python -m venv venv

# Ativar ambiente virtual - Windows
venv\Scripts\activate

# Ativar ambiente virtual - Linux
source venv\Scripts\activate

# Upgrade pip
python -m pip install --upgrade pip

# Instalação das libs
pip install apache-airflow[amazon,jdbc,celery,virtualenv,google]==2.2.2 -c "https://raw.githubusercontent.com/apache/airflow/constraints-2.2.2/constraints-3.7.txt"
```

