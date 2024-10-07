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

#### Aplicando IF com strings e lambda.
```bash
df['neighbourhood'] = df['neighbourhood_group'].apply(lambda x: 'Match' if x == 'Manhattan' else 'Mismatch')
df.head()
```

#### Aplicando IF com OR.
```bash
df.loc[(df['neighbourhood_group'] == 'Manhattan') | (df['neighbourhood_group'] == 'Brooklyn'), 'neighbourhood'] = 'Match' 
df.loc[(df['neighbourhood_group'] != 'Manhattan') & (df['neighbourhood_group'] != 'Brooklyn'), 'neighbourhood'] = 'Mismatch' 
df.head()
```

#### Aplicando uma condição IF em uma coluna.
```bash
df.loc[df['price'] <= 200, 'price_new'] = 300
df.loc[df['price'] > 200, 'price_new'] = 500
df.head()
```

#### Aplicando uma condição IF caso nulo, incluir 0.
```bash
df.loc[df['reviews_per_month'].isnull(), 'reviews_per_month'] = 0
df.head()
```

#### Ordenar dataframe em ordem crescente.
```bash
df.sort_values(by=['price'], inplace=True)
df.head()
```

#### Em ordem decrescente.
```bash
df.sort_values(by=['price'], inplace=True, ascending=False)
df.head()
```

#### Ordernar múltiplas colunas.
```bash
df.sort_values(by=['price', 'availability_365'], inplace=True)
df.head()
```

#### Substituir todos os valors NaN na coluna por 0.
```bash
df['reviews_per_month'] = df['reviews_per_month'].replace(0, np.nan).fillna(0)
df.head()
```

#### Agrupar os dados pelo neighbourhood_group.
```bash
df_counts = df.groupby('neighbourhood_group').size().reset_index(name='count')
df_counts.head()
```

#### Agrupar os dados pelo neighbourhood_group e adicionar o método shift(1) deslocandoos os valores da coluna number_of_reviews, ou seja, para cada linha, o valor da nova coluna number_of_reviews_anterior será igual ao valor da coluna number_of_reviews da linha anterior
```bash
df['number_of_reviews_anterior'] = df.groupby(['neighbourhood_group'])['number_of_reviews'].shift(1)
df.head()
```

#### Pivot: Reorganiza os dados em um formato de tabela cruzada, útil para transformar dados longos em tabulares.
```bash
pivot_df = df.pivot_table(
    index='neighbourhood_group',
    columns='room_type',
    values='price',
    aggfunc='max' 
)
pivot_df.head()
```

#### Get_dummies: Cria variáveis indicadoras (binárias) para colunas categóricas, útil na preparação de dados para análise
```bash
dummies_df = pd.get_dummies(df, columns=['room_type'])
dummies_df.head()
```

