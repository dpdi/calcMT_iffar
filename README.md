# Calculadora de Matrícula Total - IFFar

Esta ferramenta foi desenvolvida para apoiar o cálculo da **Matrícula Total** de cursos ofertados no IFFarroupilha, conforme metodologia estabelecida na **Portaria MEC nº 646/2022**.
https://iffarcalcmatriculatotal.streamlit.app/
---

## Objetivo

O projeto visa:
- Facilitar o entendimento do cálculo da Matrícula Total pelos gestores do IFFarroupilha;
- Simular cenários com diferentes parâmetros (carga horária, datas, tipo de financiamento, etc.);
- Contribuir para a análise orçamentária e correção de inconsistências nos dados cadastrados no Sistec e consequentemente, na Plataforma Nilo Peçanha.

---

## Como funciona

A calculadora segue quatro etapas principais:

1. **Equalização**  
   Ajusta o impacto dos cursos considerando duração do ciclo, carga horária e dias ativos no ano analisado.

2. **Ponderação**  
   Aplica o peso do curso(definido na Portaria).

3. **Bonificação (Agropecuária)**  
   Adiciona 50% ao valor final se o curso for da área de Agropecuária.

4. **Finalização da Matrícula Total (MT)**  
   Ajusta o valor conforme modalidade presencial ou EaD, com regras específicas de financiamento.

> Todas as fórmulas utilizadas seguem a Portaria MEC nº 646/2022 e as fórmulas da planilha da Fase 4 da Distribuição Orçamentária, gentilmente disponibilizadas pela Pró-Reitoria de Administração do IFFarroupilha.

---

## Estrutura do Projeto

- `app.py` — Código principal com interface em Streamlit.
- `correcoes_nomes.py` — Substituições padronizadas de nomes de cursos e campus.
- `4ª Fase - Conferência matrículas totais 2025 IFFARROUPILHA.csv` — Planilha com os dados de base.
- `README.md` — Este arquivo.

---

## Tecnologias Utilizadas

- [Python 3.10+](https://www.python.org/)
- [Streamlit](https://streamlit.io/) para interface web
- [Pandas](https://pandas.pydata.org/) para tratamento de dados

---

## Referência legal

Portaria MEC nº 646, de 25 de agosto de 2022  
(Institui a Matriz de Distribuição Orçamentária da Rede Federal de EPCT)

---

### 🧮 Passo a passo simplificado para calcular a Matrícula Total

**Passo 1 – Descobrir a quantidade de dias no ciclo (QTDC)**
Subtraia a data de início do ciclo (DIC) da data de término do ciclo (DTC) e adicione 1. Isso informa quantos dias o curso tem no total.

**Passo 2 – Calcular a carga horária média diária (CHMD)**
Divida a carga horária do curso (CHM) pela quantidade de dias do ciclo (QTDC). Isso mostra quanto tempo de aula ocorre por dia, em média.

**Passo 3 – Anualizar a carga horária (CHA)**
Se o curso durar mais de um ano (QTDC > 365 dias), multiplique a média diária (CHMD) por 365. Se durar até 1 ano, use a carga horária total (CHM) diretamente.

**Passo 4 – Calcular o fator de equalização da carga horária (FECH)**
Compare a CHA com o padrão de 800 horas anuais: FECH = CHA ÷ 800.

**Passo 5 – Verificar os dias ativos no ano analisado (DACP1 a DACP5)**
Dependendo das datas do ciclo e do ano de referência, calcule quantos dias do ciclo estiveram ativos no ano analisado.

**Passo 6 – Calcular o fator de equalização de dias ativos (FEDA)**
Divida os dias ativos (DACP) pela quantidade total de dias do ano (geralmente 365).

**Passo 7 – Calcular o fator combinado (FECHDA)**
Multiplique o FECH pelo FEDA. Isso ajusta o impacto do curso de acordo com sua carga horária e com o tempo de funcionamento no ano.

**Passo 8 – Calcular as Matrículas Equalizadas (MECHDA)**
Multiplique o FECHDA pela quantidade de matrículas atendidas na PNP (QTM). Esse valor é a base do cálculo da Matrícula Total.

**Passo 9 – Aplicar o peso do curso (MP)**
Multiplique o número de matrículas equalizadas (MECHDA) pelo peso do curso (PC).

**Passo 10 – Verificar se há bonificação (BA)**
Se for um curso de Agropecuária, multiplique o valor de MP por 0,5 e adicione ao total.

**Passo 11 – Calcular a Matrícula Total (MT)**
Some as Matrículas Ponderadas (MP) com a Bonificação (BA). Esse é o valor final da MT para cursos presenciais.

**Passo 12 – Ajustar para cursos EaD (se aplicável)**

* Financiamento externo: MT = MP x 0,25
* Financiamento próprio: MT = MP x 0,80