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
### Caso o CSV tenha um separador como (;), você pode especificar o saperador no código.
```bash
df = pd.read_csv('AB_NYC_2019.csv', sep=';')
df.head()
```

### Se houver problemas com o enconding do arquivo, é possível especificar o enconding.
```bash
df = pd.read_csv('AB_NYC_2019.csv', encoding='utf-8')
df.head()
```

### Para carregar apenas algumas colunas específcas.
```bash
df = pd.read_csv('AB_NYC_2019.csv', usecols=['name', 'host_name'])
df.head()
```


### Visualizar informações do DataFrame.
#### Exibe informações gerais, como o tipo de dados de cada coluna.
```bash
df.info()
```

### Descrever dados numéricos.
#### Exibe um resumo estatístico dos dados numéricos.
```bash
df.describe()
```

### Verficar a presença de valores nulos.
#### Verfica se há valores nulos no DataFrame.
```bash
df.isnull().sum()
```

### Condição IF.
#### Aplicando IF com lambda.
```bash
df['igual_ou_maior_200?'] = df['price'].apply(lambda x: 'Sim' if x <= 200 else 'Não')
df.head()
```

#### Aplicando IF com strings.
```bash
df.loc[df['neighbourhood_group'] == 'Manhattan', 'neighbourhood'] = 'Match'  
df.loc[df['neighbourhood_group'] != 'Manhattan', 'neighbourhood'] = 'Mismatch'
df.head()
```

