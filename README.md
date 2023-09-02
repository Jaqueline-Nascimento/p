# p
Transformações na planilha de frota

#Importar pandas
import pandas as pd

# Carregue o arquivo Excel ou CSV em um DataFrame, carregar no Colab 
arquivo_csv = '/content/bg16f produtividade.csv'
df = pd.read_csv(arquivo_csv, sep=',')

#Verificar as informações da planilha
df.info()

#Verificar o Cabeçalho
df.head()

#Transformar a coluna data em Data
df['Data'] = pd.to_datetime(df['Data'], format='%d/%m/%Y')

#Transformar a coluna data em formato de data para Banco de Dados
df['Data'] = df['Data'].dt.strftime('%Y-%m-%d')
