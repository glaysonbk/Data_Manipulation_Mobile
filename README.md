# Data_Manipulation_Mobile
# Import dos pacotes
import pandas as pd


# ---

# Selecao por label

# Importacao da base de dados base_best_selling_mobile_phones
df_mobile = pd.read_csv("./datasets/best_selling_mobile_phones.csv")

# Selecao da instancia com index 0 (Series)
df_mobile_i1 = df_mobile.loc[0]

# Selecao da instancia com index 0 (DataFrame)
df_mobile_i1 = df_mobile.loc[[0]]

# Selecao de apenas um atributo (model) (Series)
df_mobile_model = df_mobile.loc[:, 'model']

# Selecao de apenas um atributo (model) (DataFrame)
df_mobile_model = df_mobile.loc[:, ['model']]

# Selecao de uma lista de atributos (manufacturer, model)
df_mobile_man_mod = df_mobile.loc[:, ['manufacturer', 'model']]

# Selecao das instancias da fabricante LG
df_mobile_lg = df_mobile.loc[df_mobile['manufacturer'] == 'LG']

# Selecao das instancias da fabricante LG e dos atributos 
df_mobile_lg = df_mobile.loc[df_mobile['manufacturer'] == 'LG', ['model', 'form', 'units_sold_m']]

# Definicao do index da base de dados (model)
df_mobile_lg.set_index('model', inplace=True)

# Selecao dos atributos do index G3
df_mobile_lg_g3 = df_mobile_lg.loc[['G3']]

# Selecao do atributo form do index G3
df_mobile_lg_form_g3 = df_mobile_lg.loc['G3', 'form']

# Reseta index da base de dados
df_mobile_lg.reset_index(inplace=True)


# ---

# Selecao das instancias que apresentam numero de unidades vendidas superior a 120
df_mobile_120m = df_mobile.loc[df_mobile['units_sold_m'] > 120]

# Selecao das instancias da fabricante Samsung das vendas a partir de 2010
df_mobile_samsung_2010_hj = df_mobile.loc[(df_mobile['manufacturer'] == 'Samsung') & (df_mobile['year'] >= 2010)]

# Selecao das instancias das fabricantes Samsung ou LG
df_mobile_samsung_lg = df_mobile.loc[df_mobile['manufacturer'].isin(['Samsung', 'LG'])]

# Selecao das instancias das fabricantes Samsung ou LG ou com vendas superiores a 200
df_mobile_sam_lg_ou200 = df_mobile.loc[(df_mobile['manufacturer'].isin(['Samsung', 'LG'])) | (df_mobile['units_sold_m'] > 200)]


# ---

# Selecao por posicao

# Selecao da primeira instancia
df_mobile_i1_iloc = df_mobile.iloc[[0]]

# Selecao do primeiro atributo da primeira instancia
df_mobile_a1i1_iloc = df_mobile.iloc[0, 0]

# Selecao apenas do atributo model
df_mobile_model_iloc = df_mobile.iloc[:, [1]]

# Selecao dos tres primeiros atributos
df_mobile_3a_iloc = df_mobile.iloc[:, 0:3]

# Selecao dos tres primeiros atributos das instancias 5 a 10 (incluso)
df_mobile_3a6i_iloc = df_mobile.iloc[5:11, 0:3]


# ---

# Selecao pelo metodo query()

# Selecao das instancias da fabricante Nokia
df_mobile_nokia = df_mobile.query("manufacturer == 'Nokia'")

# Selecao das istancias que apresentam vendas superiores a 200
df_mobile_200m = df_mobile.query("units_sold_m > 200")

# Selecao das instancias da Samsung a partir de 2020
df_mobile_samsung_2020_hj = df_mobile.query("(manufacturer == 'Samsung') & (year >= 2020)")
df_mobile_samsung_2020_hj = df_mobile.query("(manufacturer == 'Samsung') and (year >= 2020)")


# Selecao das instancias das fabricantes Nokia e Apple
df_mobile_nokia_apple = df_mobile.query("manufacturer == ['Nokia', 'Apple']")
df_mobile_nokia_apple = df_mobile.query("manufacturer in ['Nokia', 'Apple']")


# Selecao das instancias que nao sao das fabricantes Nokia e Apple
df_mobile_nao_nokia_apple = df_mobile.query("manufacturer != ['Nokia', 'Apple']")
df_mobile_nao_nokia_apple = df_mobile.query("manufacturer not in ['Nokia', 'Apple']")


# Selecao das instancias das fabricantes Motorola e Xiaomi ou com vendas inferiores a 5
df_mobile_moto_xiaomi = df_mobile.query("(manufacturer in ['Motorola', 'Xiaomi']) or (units_sold_m < 5)")

# Renomeacao de labels de atributos
df_mobile = df_mobile.rename(columns={"units_sold_m":"unidades_vendidas_m"})


# ---

# Remocao do atributo manufacturer
df_mobile_nokia = df_mobile.query("manufacturer == 'Nokia'")
df_mobile_nokia = df_mobile_nokia.drop(columns=['manufacturer'])

# Remocao do index Bar (form)
df_mobile_nokia = df_mobile_nokia.set_index('form')
df_mobile_nokia = df_mobile_nokia.drop(index=['Bar'])


# ---

# Amostragem

# Amostragem definindo o numero de amostras
df_mobile_10i = df_mobile.sample(n=10)

# Amostragem definindo o percentual do numero de instancias da base
df_mobile_30pct = df_mobile.sample(frac=0.30)
