
#Tirar ruídos

def validar_temperatura(t):

    return -100 <= t <= 120



# Classificação

def classificar_termica(t):

    if t < -40: return "Cold Case Crítico"

    elif t < -20: return "Frio (Atenção)"

    elif t <= 50: return "Nominal (Ideal)"

    elif t <= 70: return "Quente (Atenção)"

    else: return "Hot Case Crítico"



#Máxima e mínima

def picos_vales(lista):

    return max(lista), min(lista)



#Diagnóstico final

def gerar_relatorio(lista):

    pico, vale = picos_vales(lista)

    print(f"    Diagnóstico de Saúde do Satélite")

    print(f"Máxima: {pico:.1f}°C | Mínima: {vale:.1f}°C")

    print(f"Status Final: {classificar_termica(lista[-1])}")



def main():

    tempos = list(range(0, 153, 3)) #Criação dos 50 pontos

    temperaturas_limpas = []



    for t in tempos:

      #De acordo com a órbita

        temp_simulada = 20 + 60 * math.sin(t / 20)



#Usar apenas não-ruídos

        if validar_temperatura(temp_simulada):

            temperaturas_limpas.append(temp_simulada)



#Gráfico

    plt.plot(tempos, temperaturas_limpas, color='red')

    plt.title("Monitoramento LEO - 500km")

    plt.grid(True)

    plt.show()



    gerar_relatorio(temperaturas_limpas)



main()