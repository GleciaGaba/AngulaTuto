#AngularTuto
Angular Tuto

Pour aider à la compréhension, nous avons suivi le tutoriel Angular. 
Pour commencer, nous avons aussi créé un environnement de travail sur VSCODE, afin de travailler avec le framework Angular. 

Angular nous permet de créer applications avec nous composants.

Voici un résumé de ma compréhension de l'utilisation du framework Angular: 

1. Création d'une liste :

 Création d'une liste de produits, avec la création d'une <div>  et *ngFor, pour faire répéter chaque produit de la liste.  On a aussi utilisé *ngIf pour ancrer l'insertion du template. 

2. Passé les données à un composant enfant :

Création d'un alerte qui vérifie si les prix des produits est > $700. 
Si le prix est > $700 le client doit recevoir une notification. 

Pour créer cette notification, on a utilisé :
-ng generate component product-alerts 

Le code a fourni des fichiers enfants de ProductList Component. 
Dans le fichier ts, on trouve une classe avec les metadata sur le composant (selector, templates et styles).

@component() - configuration metadata qui détermine comme le composant doit être traité.

Pour faire ProductAlertsComponents recevoir les données du produit, il faut les importer à partir de @angular/core.

Avec un nouveau code écrit dans le terminal, un dossier AppModule sera ajouté. Il permet la validation d'autres composants dans l'application. 

ProductAlertsComponents déviant un enfant de ProductListComponent.

3. Passer les données à un composant parent :

Pour la création d'un bouton "Notify Me button", l'enfant composant a besoin de passé la donnée au composant parent.

ProducAlertComponent envoie un "event" quand "Notify Me" est cliqué, et ProductListComponent a besoin de répondre  à l' "event". 

4. Ajout de navigation :

Ajout de fonctionnalités à l'application.
Type à URL (association d'un chemin URL au composant)
Click links
click  browser aller/retour 
Création d'un dossier Product-details, avec un code sur le terminal. 


5. Voir les détails du produit :

Le composant ProductDetailsComponent gère l'affichage de chaque produit. Le routeur Angular affiche les composants en fonction de l'URL du navigateur et des routes que vous avez définies.

On a fait la combinaison des données de produits et la route pour les informations envoyées à l'écran. 

Les paramètres de route correspondent au chemin qui on a défini sur la route. ActivatedRouteSnapshot contient des informations sur l'activation de la route.

Lorsque les utilisateurs cliquent sur un nom de produit dans la liste, le router les dirige vers l'URL. 

6. Managing Data:

Dans cette partie, l'application a un catalogue de produits avec deux parties. Une liste de produits et leurs détails.

Dans cette partie, on doit créer un "shopping cart", avec l'objectif de :

- Faire la mise à jour 
- Additionner les composants du panier 
- Additionner un composant d'expédition 

7. Création du "shopping cart":

Un service est une instance de la classe qui peut être disponible de quelque partie de l'application, dans ce cas on utilise  "Angular's dependency injection system". 

Pour commencer on a créé une manière d'ajouter les produits dans le panier.  Avec l'objectif d'ajouter un bouton pour acheter et garder les informations d'achat . 

On utilise un code dans le terminal pour la création d'un dossier "CartService". 

ng generate service cart 

Suite l'importation de l'interface de Product   à partir de ./products.ts dans "cart.service.ts" fichier. Ainsi que la définition de la méthode pour ajouter les items dans le panier. 
addToCart() - méthode qui ajoute un produit à un tableau d'élements.
getItems() - méthode qui collecte les items avec la quantité associée.
clearCart() -méthode qui retourne un tableau vide. 
8. Le service de Panier

Il faut importer les informations dans product-details.components.

import { Product, products } from '../products';
import { CartService } from '../cart.service';

Création du service dans uns constructeur dans product-details.component.ts. 

Et insertion d'un bouton dans avec l'évent clique dans product-details.component.html.

9.Création de la "cart view"

- Création d'un cart composant et la configuration de la route.
- Affichage de la cart. 

10. Ajout du composant cart avec le code sur le terminal.

ng generate component cart

Dans le fichier, il avait déjà le code pour importer le composent.  Il a aussi ajouté le CartComposant dans app.mudule.ts.
La création d'une route pour le CartComponent dans app.mudule. 

{ path: 'cart', component: CartComponent },

Mise à jour du bouton de checkout.

11. Affichage des "cart items" 

Pour afficher les produits dans le panier, il faut importer le CartService à partir  cart.service.ts fichier. Insertion  de CartService dans construteur. 
Definition de la propriété items dans la classe pour garder les informations du panier. 

 items = this.cartService.getItems();

"This code sets the items using the CartService getItems() method. You defined this method when you created cart.service.ts."

Mise à jour du template en utilisant  <div> avec *ngFor, pour afficher les produits dans le panier. 

12. Récupération du prix d'expédition
Dans cette partie, on commence à travailler avec APIs, pour récupérer les prix d'expéditions des produits. 

13. Configuration de AppModule pour utiliser HttpClient. 

L'importation de HttpClientModule à partir de '@angular/common/http' et enregistrement dans @NgModule(). 


14. Configuration de CartService pour l'utilisation de HttpClient.

Installation de HttpClient  à l'application, avec l'importation et insertion de HttpClient dans le construteur. 

15. Configuration de la CartService pour avoir les prix d'expédition. 

Pour récupérer les données  à partir de 
shipping.json, on doit utiliser HttpClient avec le get() méthode. 

Définition d'un nouveau méthode getShippingPrices().

16. Création d'un composent d'expédition. 

Création d'un nouveau dossier avec shipping.components. 
Ajout d'un chemin pour ShippingComponent dans app.module.ts. 

17. Configuration pour ShippingComponent pour l'utilisation de CartService. 

Importation de CartService dans shipping.component.ts et insertion dans du cartService dans le constructeur.
Utilisation de la méthode getShippingPrices(). 

shippingCosts = this.cartService.getShippingPrices();

Et mise à jour de ShippingComponent, en utilisant async pipe dans shipping.component.html.

Async pipe retourne le dernier flux de donnée, pendant toute la vie du composant. 
Ajout du link dans CartComponent, pour la visualisation de ShippingComponent. 

18. Utiliser des formulaires pour la saisie de l'utilisateur. 

Ajout d'une fonctionnalité de paiement, avec un formulaire pour colleter des informations sur l'utilisateur. 

Importation de FormBuilder à partir de @angular/forms et insertion dans le constructeur. 

constructor(
    private cartService: CartService,
    private formBuilder: FormBuilder,
 ) {}


Utilisation de la méthode group() pour donner à checkoutForm propriété le modèle qui contient le nom et adresse. 

checkoutForm = this.formBuilder.group({
    name: '',
    address: ''
  });

Définition de la méthode onSubmit() pour intégrer le formulaire.  Cette méthode permet que les utilisateurs puissent envoyer leurs  nomes et adresses.  on utilise aussi la méthode clearCart() pour nettoyer le panier. 


19. Création d'un formulaire de paiement

Ajout d'un formulaire de paiement dans  la partie de bas du panier. 

En bas dans cart.component.html, ajouter HTML <form>  bouton.  Dans la balise form, on doit ajouter ngSubmit , avec un évent pour soumission et appelle de ma méthode  onSubmit(). 

Ajout des inputs name et adress. 
<div>
    <label for="name">
      Name
    </label>
    <input id="name" type="text" formControlName="name">
  </div>

Après avoir mis des produits dans le panier, les utilisateurs peuvent rentrer ses coordonnés. 



 




  







 







