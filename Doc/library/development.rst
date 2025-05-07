import matplotlib.pyplot as plt
import numpy as np
from matplotlib.backends.backend_pdf import PdfPages

# Dados de rendimento de milho (em t/ha)
anos = ['2021', '2022', '2023']
tratamentos = ['Controle', 'N80', 'GM_2M', 'GM_2.5M', 'GM_3M']
rend_milho = [
    [7.20, 8.30, 8.50, 8.60, 8.75],  # 2021
    [1.61, 2.40, 3.70, 3.75, 4.10],  # 2022
    [11.80, 11.85, 11.95, 12.00, 12.11]  # 2023
]

# Dados de precipitação em outubro e biomassa correspondente
prec_outubro = [197.3, 1.7, 15.4]  # mm para os anos 2020, 2021 e 2022
biomass_media = [12.27, 0.76, 3.07]  # média de biomassa por ano

# Criar o arquivo PDF
with PdfPages("Relatorio_Adubacao_Verde_Graficos.pdf") as pdf:
    
    # Gráfico 1: Rendimento de milho por tratamento e ano
    fig1, ax1 = plt.subplots(figsize=(10, 6))
    x = np.arange(len(anos))
    width = 0.15
    for i in range(len(tratamentos)):
        valores = [rend_milho[ano][i] for ano in range(len(anos))]
        ax1.bar(x + i * width, valores, width, label=tratamentos[i])
    
    ax1.set_title('Rendimento de milho por tratamento e ano')
    ax1.set_xlabel('Ano')
    ax1.set_ylabel('Rendimento (t/ha)')
    ax1.set_xticks(x + 2 * width)
    ax1.set_xticklabels(anos)
    ax1.legend(title='Tratamento')
    plt.tight_layout()
    pdf.savefig(fig1)
    plt.close(fig1)

    # Gráfico 2: Correlação entre precipitação em outubro e biomassa
    fig2, ax2 = plt.subplots(figsize=(10, 6))
    ax2.scatter(prec_outubro, biomass_media, color='green', s=100)
    for i, year in enumerate(['2020', '2021', '2022']):
        ax2.annotate(year, (prec_outubro[i], biomass_media[i]), textcoords="offset points", xytext=(0,10), ha='center')
    
    ax2.set_title('Correlação entre precipitação em outubro e biomassa de ervilhaca')
    ax2.set_xlabel('Precipitação em outubro (mm)')
    ax2.set_ylabel('Biomassa média (t/ha)')
    plt.tight_layout()
    pdf.savefig(fig2)
    plt.close(fig2)

print("✅ PDF gerado: Relatorio_Adubacao_Verde_Graficos.pdf")
.. _development:

*****************
Development Tools
*****************

The modules described in this chapter help you write software.  For example, the
:mod:`pydoc` module takes a module and generates documentation based on the
module's contents.  The :mod:`doctest` and :mod:`unittest` modules contains
frameworks for writing unit tests that automatically exercise code and verify
that the expected output is produced.

The list of modules described in this chapter is:


.. toctree::

   typing.rst
   pydoc.rst
   devmode.rst
   doctest.rst
   unittest.rst
   unittest.mock.rst
   unittest.mock-examples.rst
   test.rst
