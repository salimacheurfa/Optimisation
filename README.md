
# Optimisation

Cet algorithme simule un modèle physique, ajoute du bruit blanc au signal, et utilise une méthode d'optimisation (gradient) pour ajuster les paramètres du modèle afin de minimiser l'erreur entre le signal bruité et le modèle ajusté. Il trace ensuite les signaux pour visualiser la performance de l'optimisation.

## Exercice 1 : modélisation d’un système physique
### Étape 1 : Initialisation et Préparation 
'''bash
clear all
close all 
clc
'''
On commence par nettoyer l'environnement de travail, fermer toutes les figures ouvertes et effacer la console.

### Étape 2 : Définition des paramètres de simulation
'''bash 
t = 0:0.1:100;
precis = 1e-5;
alpha = 1e-2;
'''
On définit le vecteur temps allant de 0 à 100 avec un pas de 0.1.
On fixe la précision à 10^(-5) pour la convergence.
On fixe le taux d'apprentissage (alpha) à 10^(-2).

### Étape 3 : Simulation du modèle initial
'''bash
A1 = 1.7;
B1 = 0.5;
A3 = 2.5;
B3 = 0.1;

y = A1*exp(-B1*t) + A3*exp(-B3*t);
'''
On initialise les paramètres du modèle 𝐴1, B1, A3, B3.
On calcule la sortie y du modèle sans bruit.

### Étape 4 : Ajout de bruit blanc
'''bash
br = sqrt(0.09)*randn(size(t));
yb = br + y;
'''
On génère du bruit blanc de variance 0.09.
On ajoute ce bruit à y pour obtenir yb, la version bruitée de notre signal.

### Étape 5 : Tracé initial des signaux
'''bash
figure(1) 
plot(t,y,'b');
hold on;
plot(t,yb,'k');
hold on;
'''
On trace le signal original y en bleu.
On trace le signal bruité yb en noir sur la même figure.

### Étape 6 : Initialisation des paramètres pour l'optimisation
'''bash
A11 = 1;
B11 = 1;
A33 = 1;
B33 = 1;
num_iterations = 0;
e = inf;
'''
On initialise les paramètres A11, B11, A33, B33 pour l'optimisation.
On initialise le compteur d'itérations et l'erreur e.

### Étape 7 : Boucle d'optimisation
'''bash
while e > precis
  ym = A11 * exp(-B11 * t) + A33 * exp(-B33 * t);
  error = ym - yb;
  
  dA11 = sum(2 * error .* exp(-B11 * t));
  dB11 = sum(2 * error .* (-A11 * t .* exp(-B11 * t)));
  dA33 = sum(2 * error .* exp(-B33 * t));
  dB33 = sum(2 * error .* (-A33 * t .* exp(-B33 * t)));
  
  A11 = A11 - alpha * dA11;
  B11 = B11 - alpha * dB11;
  A33 = A33 - alpha * dA33;
  B33 = B33 - alpha * dB33;
  
  error1 = A11 * exp(-B11 * t) + A33 * exp(-B33 * t) - yb;
  e = max(abs(error1 - error));
  
  num_iterations = num_iterations + 1;
  plot(t, ym, 'r');
end
'''
#### Calcul du modèle 
On calcule la sortie actuelle du modèle avec les paramètres courants.
#### Calcul de l'erreur
 On calcule l'erreur entre le modèle actuel et le signal bruité.
#### Calcul des gradients
On calcule les gradients des paramètres.
#### Mise à jour des paramètres
On met à jour les paramètres en utilisant les gradients.
#### Calcul de la nouvelle erreur 
On calcule l'erreur après mise à jour.
####Vérification de la convergence
On vérifie si l'erreur est inférieure à la précision souhaitée.
#### Incrémentation et tracé
On incrémente le compteur d'itérations et on trace la sortie actuelle du modèle en rouge.

### Étape 8 : Affichage des résultats finaux
'''bash 
ym_final = A11 * exp(-B11 * t) + A33 * exp(-B33 * t);

figure(3) 
plot(t, y, 'b', 'DisplayName', 'y(t) original');
hold on;
plot(t, ym_final, 'g', 'DisplayName', 'ym(t) identifié');
legend;
'''
On calcule la sortie finale du modèle avec les paramètres optimisés.
On trace le signal original y en bleu et le signal identifié 𝑦𝑚 𝑓𝑖𝑛𝑎𝑙 en vert sur une nouvelle figure avec une légende pour distinguer les deux.



## Acknowledgements

 - [Awesome Readme Templates](https://awesomeopensource.com/project/elangosundar/awesome-README-templates)
 - [Awesome README](https://github.com/matiassingers/awesome-readme)
 - [How to write a Good readme](https://bulldogjob.com/news/449-how-to-write-a-good-readme-for-your-github-project)


## API Reference

#### Get all items

```http
  GET /api/items
```

| Parameter | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `api_key` | `string` | **Required**. Your API key |

#### Get item

```http
  GET /api/items/${id}
```

| Parameter | Type     | Description                       |
| :-------- | :------- | :-------------------------------- |
| `id`      | `string` | **Required**. Id of item to fetch |

#### add(num1, num2)

Takes two numbers and returns the sum.


## Authors

- [@octokatherine](https://www.github.com/octokatherine)


## Badges

Add badges from somewhere like: [shields.io](https://shields.io/)

[![MIT License](https://img.shields.io/badge/License-MIT-green.svg)](https://choosealicense.com/licenses/mit/)
[![GPLv3 License](https://img.shields.io/badge/License-GPL%20v3-yellow.svg)](https://opensource.org/licenses/)
[![AGPL License](https://img.shields.io/badge/license-AGPL-blue.svg)](http://www.gnu.org/licenses/agpl-3.0)


## Demo

Insert gif or link to demo


## FAQ

#### Question 1

Answer 1

#### Question 2

Answer 2


## 🚀 About Me
I'm a full stack developer...


## 🔗 Links
[![portfolio](https://img.shields.io/badge/my_portfolio-000?style=for-the-badge&logo=ko-fi&logoColor=white)](https://katherineoelsner.com/)
[![linkedin](https://img.shields.io/badge/linkedin-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/)
[![twitter](https://img.shields.io/badge/twitter-1DA1F2?style=for-the-badge&logo=twitter&logoColor=white)](https://twitter.com/)


## 🛠 Skills
Javascript, HTML, CSS...


## Lessons Learned

What did you learn while building this project? What challenges did you face and how did you overcome them?


## Roadmap

- Additional browser support

- Add more integrations


## Related

Here are some related projects

[Awesome README](https://github.com/matiassingers/awesome-readme)

