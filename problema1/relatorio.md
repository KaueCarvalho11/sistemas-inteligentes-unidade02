# Necessidade de Normalização 

A rede Adaline ajusta seus pesos por meio da Regra Delta, que corrige os erros passo a passo usando os próprios valores numéricos das entradas para encontrar o menor erro possível. Quando os dados possuem escalas muito diferentes ou médias distantes de zero, os atributos com números maiores acabam dominando essas correções, o que torna o espaço de busca desproporcional e faz com que o algoritmo dê passos desequilibrados, oscilando fortemente ou até perdendo o controle e divergindo durante o treino. Ao aplicar a padronização Z-score, todos os atributos são ajustados para ficarem na mesma faixa de grandeza, equilibrando a influência de cada entrada nas atualizações e garantindo que o aprendizado ocorra de forma estável, suave e uniforme até a melhor solução.

# Escolha do valor de n

No primeiro gráfico, foi possível identificar que as taxas de aprendizagem mais altas (0,05 e 0,1) divergem e fazem o erro explodir. Porém, como esse aumento disparou a escala do gráfico, as demais curvas ficaram achatadas no fundo, impedindo de enxergar qual delas era a melhor. Por isso, foi preciso plotar um segundo gráfico dando zoom apenas nas taxas estáveis (0,0001, 0,001 e 0,01). Esse segundo gráfico confirmou que 0,001 é o valor ideal, pois sua curva desce de forma suave e atinge o menor erro final.

# Erro mais crítico

O erro mais crítico é classificar um sinal ruim como se fosse bom (falso positivo para a classe good). Como a classe ruim indica falha de transmissão ou interferência, o sistema acharia que o canal está funcionando normalmente quando, na verdade, há um problema, deixando de acionar alertas ou correções e causando perda de dados ou falhas na operação. 
