import streamlit as st
import pandas as pd
import matplotlib.pyplot as plt

st.title('CRAS CORONEL XAVIER CHAVES')


st.header('BANCO DE CADASTRO')

dados = st.file_uploader('Carregar dados')
if dados is not None:
    df = pd.read_csv(dados,sep=',')

else:
    df = []
st.dataframe(df)


st.sidebar.header('CADASTRAR USUARIO')


if dados is not None:
    #st.bar_chart(df, x='Regiao', y='Necessidades por regiao')
     fig, ax = plt.subplots()
     ax.hist(df['Regiao'], bins=10)
     ax.set_ylabel("NECESSIDADES POR REGIAO")
     ax.set_xlabel("REGIAO")

     st.pyplot(fig)


FORMULARIO = st.sidebar.form('Formulario',clear_on_submit=True)
novo_nome = FORMULARIO.text_input('NOME')
nova_idade = FORMULARIO.text_input('IDADE')
novo_cpf = FORMULARIO.text_input('CPF')
nova_identidade = FORMULARIO.text_input('IDENTIDADE')
novo_endereco = FORMULARIO.text_input('ENDEREÇO')
nova_deficiencia = FORMULARIO.text_input('DEFICIENCIA')
nova_regiao = FORMULARIO.text_input('REGIÃO')
nova_necessidade = FORMULARIO.text_input('NECESSIDADES POR REGIÃO')


bt1 = FORMULARIO.form_submit_button('Enviar')
if bt1:
    novo = {'Nome': [novo_nome],
            'Idade': [int(nova_idade)],
            'CPF': [int(novo_cpf)],
            'Identidade': [nova_identidade],
            'Endereco': [novo_endereco],
            'Deficiencia': [nova_deficiencia],
            'Regiao': [nova_regiao],
            'Necessidades por regiao': [nova_necessidade]}

    x = pd.DataFrame(novo)  # CRIAR NOVO DATAFRAME
    DF = pd.concat([df, x],ignore_index = True)
    st.dataframe(DF)

# SALVA OS NOVOS DATAFRAME

    DF.to_csv('C:/aula_python/Dados.csv',index = False, mode = 'w')
 
