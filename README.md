import pandas as pd
import numpy as np

# Criando o DataFrame
data = {
    'Data': ['15/01/2025', '15/01/2025', '15/01/2025', '15/01/2025', '15/01/2025'],
    'Cidade': ['São Paulo', 'Rio de Janeiro', 'Curitiba', 'Porto Alegre', 'Salvador'],
    'Temperatura Máxima (°C)': [30.5, 35.0, 24.0, 28.0, 31.0],
    'Temperatura Mínima (°C)': [22.0, 25.0, 18.0, 20.0, 24.5],
    'Precipitação (mm)': [12.0, np.nan, 8.0, 15.0, np.nan],
    'Umidade Relativa (%)': [78, 70, np.nan, 82, 80]
}

df = pd.DataFrame(data)

# Substituindo valores ausentes na coluna Precipitação pela média
media_precipitacao = df['Precipitação (mm)'].mean()
df['Precipitação (mm)'].fillna(media_precipitacao, inplace=True)

# Substituindo valores ausentes na coluna Umidade Relativa pela mediana
mediana_umidade = df['Umidade Relativa (%)'].median()
df['Umidade Relativa (%)'].fillna(mediana_umidade, inplace=True)

# Adicionando a coluna Amplitude Térmica
df['Amplitude Térmica'] = df['Temperatura Máxima (°C)'] - df['Temperatura Mínima (°C)']

# Criando um novo DataFrame com cidades que têm Temperatura Máxima acima de 30°C
df_high_temp = df[df['Temperatura Máxima (°C)'] > 30]

# Reordenando as colunas
df = df[['Data', 'Cidade', 'Temperatura Máxima (°C)', 'Temperatura Mínima (°C)', 'Amplitude Térmica', 'Precipitação (mm)', 'Umidade Relativa (%)']]

print(df)
print(df_high_temp)
