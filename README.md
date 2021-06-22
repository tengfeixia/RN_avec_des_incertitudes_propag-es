# RN_avec_des_incertitudes_propag-es
C'est le fruit de travaille pendant mon stage de M1
J'ai crée des RN afin de permettre les incertitudes propagées. Donc le output sera les valeurs prédites accompangé avec ses incertitudes/erreurs.

Les incertitudes sont défines par les variances. 
Par exemple, on voit souvent que un résultat de mesure sont doonée par x = 1.2±0.2, avec k=2 au niveau de confiance 95%
Dans ce cas, la variance vaut 0.1 et les incertitudes sont 0.2

Pour faire des incertituces propagées, dans le cas non-coréles, il faut utiliser W*W pour faire une propagation feed-forward.
Sachant que les poids W ont l'ordre grandeur 0.1, donc l'ordre de grandeur vaut W^2.
Donc les incertitudes devient 0.01 fois petits passant chaque couche de mon RN, qui sont très faible à la couche de la sortie. (l'ordre grandeur 1e-8 pour un RN avec 4 couches) 
Par conséquence, les incertitudes relatives sont hypergrandes. À cause des fonction d'activaion, on ne peut pas trainer notre RN choissant notre fonction de perte comme MSE relatives. 


Donc j'essaie de utiliser les "erreurs" de mesure au lieu de "incertitudes".
Par exemple pour y = 2x, si on trouve x=1.01 au lieu de 1 (vraie valeur), on aura 0.02 d'erreur pour y  à la fin
            pour y= 3x, sin on trouve x=0.99 au lieu de 1, on aura à la fin -0.03 d'erreur à la fin 
            
L'avantage d'utiliser "erreur" c'est que l'on peut utiliser W (au lieu de W^2) pour faire une propagation feed-forward. 
Dans ce cas, les "erreurs" trouvées à la dernière couche sera l'order 1e-4 pour un RN avec 4 couches donc les erreurs relatives sont faibles et possible à trainer.

            

