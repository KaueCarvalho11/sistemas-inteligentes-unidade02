# Discussão sobre balanceamento

O conjunto de dados é razoavelmente balanceado, com 27.000 imagens distribuídas entre 10 classes que variam de 2.000 amostras (Pasture, 7,41%) a 3.000 amostras (AnnualCrop, Forest, HerbaceousVegetation, Residential e SeaLake, 11,11% cada), enquanto as demais possuem 2.500 imagens (9,26%). Essa diferença máxima de apenas 1,5 vez entre as classes maiores e a menor indica ausência de desbalanceamento severo, dispensando técnicas de reamostragem e exigindo apenas a divisão estratificada para manter essas proporções nos conjuntos de treino, validação e teste.   

# Análise das curvas

As curvas de loss e acurácia mostram que o modelo converge rapidamente nas primeiras épocas, atingindo o menor erro de validação na época 9. A partir da época 10, fica evidente o fenômeno de overfitting: enquanto a loss de treino continua caindo até se estabilizar próxima de zero e a acurácia de treino se aproxima do máximo, a loss de validação passa a subir de forma consistente e a acurácia de validação estagna, gerando um distanciamento crescente entre as curvas. Esse comportamento indica que a rede passou a memorizar ruídos e particularidades do conjunto de treino em vez de melhorar sua capacidade de generalização, o que justifica o early stopping com a restauração dos pesos da época 9 (ponto de menor erro de validação) para a avaliação final.

# Três pares de classes mais confundidos entre sí

Os três pares de classes mais confundidos entre si são HerbaceousVegetation e PermanentCrop, Highway e River, e AnnualCrop e PermanentCrop. No primeiro caso (HerbaceousVegetation e PermanentCrop), a confusão ocorre provavelmente porque ambas as classes apresentam áreas de vegetação com cores e texturas muito parecidas (tons de verde e marrom misturados) e sem construções urbanas, o que dificulta a diferenciação visual. No segundo par (Highway e River), o erro acontece provavelmente porque ambas aparecem nas imagens como faixas estreitas e alongadas cortando a paisagem, sugerindo que a rede confunde estradas com rios por terem formatos geométricos semelhantes. Já no terceiro par (AnnualCrop e PermanentCrop), a troca de rótulos indica que a rede tem dificuldade em separá-las porque ambas representam áreas de plantação divididas em formatos retangulares e regulares, compartilhando padrões visuais e cores muito próximos

# Comparação entre os modelos

Com o uso de data augmentation, a distância entre as curvas de treino e de validação diminuiu drasticamente ao longo das 30 épocas: enquanto no modelo original as curvas se afastavam após a época 9 (indicando overfitting), no modelo com augmentation ambas caminharam próximas até o final, permitindo que a rede continuasse aprendendo e atingisse a menor loss de validação apenas na época 28. No conjunto de teste, houve um salto expressivo de desempenho, com a acurácia global subindo de 89,43% para 94,42% e o F1-score macro passando de 0,8912 para 0,9430. Nos três pares de classes mais confundidos anteriormente, os erros caíram de forma consistente: entre HerbaceousVegetation e PermanentCrop reduziram de 61 para 22 casos; entre Highway e River, de 36 para 25; e entre AnnualCrop e PermanentCrop, de 33 para 26.

# Adequação para imagens de satélite

Espelhamentos horizontais, verticais e rotações aleatórias são adequados para imagens de satélite porque essas cenas são capturadas de cima e não possuem uma orientação fixa, de modo que girar ou espelhar uma floresta, rodovia ou plantação preserva completamente sua classe sem distorcer o significado semântico da imagem.

# O motivo de não aplicar ao conjunto de validação e teste

Isso se dá porque esses conjuntos precisam refletir fielmente os dados reais originais e permanecer fixos e determinísticos para garantir uma avaliação justa, estável e reprodutível da capacidade de generalização do modelo