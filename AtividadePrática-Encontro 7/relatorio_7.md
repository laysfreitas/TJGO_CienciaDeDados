### Conclusão Kit 8

O desafio demonstrou com sucesso que é possível construir um modelo preditivo útil com poucas, mas boas, características. O resultado de 78.21% de acurácia com apenas `Pclass` e `Sex` valida a relevância dessas variáveis.


### Conclusão Kit 9

O modelo de Árvore de Decisão, apesar de mais complexo, não trouxe um ganho expressivo de performance em relação ao modelo de Regressão Logística que usava apenas duas variáveis. Isso reforça a conclusão anterior de que Pclass e Sex são as características mais dominantes para este problema.

### Conclusão Kit 10

A otimização do hiperparâmetro max_depth foi uma etapa crucial e bem-sucedida, elevando a acurácia do modelo para 80.45%. O experimento identificou que a profundidade ótima para a Árvore de Decisão é 4.

### Conclusão Kit 11

A performance estagnada sugere que o modelo atingiu sua capacidade máxima de aprendizado com poucas árvores (10 ou menos). A principal característica do Random Forest é sua resistência ao overfitting pelo simples aumento de árvores; adicionar mais árvores após um certo ponto não melhora nem piora a performance, apenas aumenta o custo computacional. Foi exatamente o que aconteceu aqui: o modelo convergiu rapidamente para seu resultado ótimo e ali permaneceu.