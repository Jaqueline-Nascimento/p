# p
#Transformações na planilha de frota, renomeando as colunas, alterando o formato de data para o formato de banco de datas, e colocando a data como DateTime, transformando as colunas de % em Float

#Importar pandas
import pandas as pd

# Carregue o arquivo Excel ou CSV em um DataFrame, carregar no Colab 
from google.colab import files
import pandas as pd

# Faça o upload do arquivo CSV
uploaded = files.upload()

# Obtenha o nome do arquivo carregado (isso funcionará mesmo que você tenha carregado vários arquivos)
nome_do_arquivo = list(uploaded.keys())[0]

# Carregue o arquivo CSV em um DataFrame
df = pd.read_csv(nome_do_arquivo)
# Supondo que 'df' seja o seu DataFrame

# Renomeie as colunas
df = df.rename(columns={
    'GerÃªncia': 'Gerencia',
    'ServiÃ§o': 'Servico',
    'Local de ApresentaÃ§Ã£o': 'Local de Apresentacao',
    'GuarniÃ§Ã£o': 'Guarnicao',
    'UtilizaÃ§Ã£o': 'Utilizacao',
    'Tipo de ApresentaÃ§Ã£o': 'Tipo de Apresentacao',
    '(%)Capacidade UtilizaÃ§Ã£o (Peso)': '(%)Capacidade Utilização (Peso)',
    '(%)UtilizaÃ§Ã£o (Tempo)': '(%)Capacidade Utilização (Tempo)'
})

# Agora, as colunas foram renomeadas

df.info()

# Substitua "NAN%" por "0" na coluna específica
coluna_P = '(%)Capacidade Utilização (Peso)'
df[coluna_P] = df[coluna_P].str.replace('NAN%', '0')

# Suponha que você deseja fazer a mesma substituição em outra coluna, como 'coluna_Tempo'
coluna_Tempo = '(%)Capacidade Utilização (Tempo)'
df[coluna_Tempo] = df[coluna_Tempo].str.replace('NAN%', '0')

df.head(3)

# Suponha que você já carregou seus dados em um DataFrame chamado 'df'
# Certifique-se de ter importado os dados primeiro

# Remove o "%" da coluna e a converte para float
coluna_P = '(%)Capacidade Utilização (Peso)'
df[coluna_P] = df[coluna_P].str.replace('%', '').astype(float)

# Remove o "%" da coluna e a converte para float
coluna_Tempo = '(%)Capacidade Utilização (Tempo)'
df[coluna_Tempo] = df[coluna_Tempo].str.replace('%', '').astype(float)

df.head(3)

import pandas as pd

# Suponha que a coluna 'Data' esteja no formato 'dd/mm/yyyy', você pode usar o formato correspondente
df['Data'] = pd.to_datetime(df['Data'], format='%d/%m/%Y')

# Agora a coluna 'Data' estará no formato de data

#Transformando para data no formado banco de dados
df['Data'] = df['Data'].dt.strftime('%Y-%m-%d')

import pandas as pd

# Supondo que 'df' seja o seu DataFrame transformando em data novamente
df['Data'] = pd.to_datetime(df['Data'], format='%Y-%m-%d')

df.info()

#EXPORTANDO A TABELA 
from google.colab import files

# Supondo que 'df' seja o seu DataFrame modificado

# Salve o DataFrame modificado como um arquivo CSV
df.to_csv('bge_produtividade_tratada.csv', index=False)

# Faça o download do arquivo usando a biblioteca 'files'
files.download('bge_produtividade_tratada.csv')
