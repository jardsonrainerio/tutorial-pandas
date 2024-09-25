# Tutorial de Pandas

Este tutorial contém exemplos práticos de como utilizar o Pandas para manipulação de dados com Python.

## Instalação

Para instalar o pandas, use o pip:

```bash
pip install pandas
```
## Criando um DataFrame com Pandas.
### Digitando os valores no próprio Python para criar DataFrame.
```bash
import pandas as pd

data = {'Nome': ['Ana', 'João', 'Maria'], 'Idade': [28, 34, 29]}
df = pd.DataFrame(data)
df.head()
```

### Ou importando os dados de uma arquivo CSV.
```bash
import pandas as pd

df = pd.read_csv('AB_NYC_2019.csv')
df.head()
```


