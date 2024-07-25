# Marmytho - Un site créé pour pratiquer Symfony 7

## Installation

1. Créer un projet Symfony 7.1

```bash
symfony new marmytho --version="7.1.*"  --webapp
```

2. Créer un certificat auto-signé pour le serveur de développement

```bash
symfony server:ca:install
```

3. Démarrer le serveur de développement

```bash
symfony serve -d
```

4. Ouvrir le navigateur à l'adresse https://localhost:8000

## Development

1. Créer un contrôleur

```bash
symfony console make:controller IngredientController
```

2. Créer une entité

```bash
symfony console make:entity Ingredient
```

3. Créer la base de données

```bash
symfony console doctrine:database:create
```

4. Créer une migration

```bash
symfony console make:migration
```

5. Exécuter la migration

```bash
symfony console doctrine:migrations:migrate
```

6. Créer un formulaire

```bash
symfony console make:form IngredientType
```

7. Dans le Controller créer :

-   Une méthode `list()` pour afficher la liste des ingrédients
-   Une méthode `show()` pour afficher un ingrédient
-   Une méthode `new` pour afficher le formulaire de création d'un ingrédient
-   Une méthode `edit` pour afficher le formulaire de modification d'un ingrédient
-   Une méthode `delete` pour afficher la suppression d'un ingrédient

Exemple de méthode `new` :

```php
use App\Form\IngredientType;
use Symfony\Component\HttpFoundation\Request;
use Symfony\Component\HttpFoundation\Response;
use Symfony\Component\Routing\Annotation\Route;

#[Route('/ingredient')]
public function new(Request $request, EntityManager $em): Response
{
    $ingredient = new Ingredient();
    $form = $this->createForm(IngredientType::class, $ingredient);
    $form->handleRequest($request);

    if ($form->isSubmitted() && $form->isValid()) {
        $em->persist($ingredient);
        $em->flush();

        return $this->redirectToRoute('ingredient_index');
    }

    return $this->render('ingredient/new.html.twig', [
        'ingredient' => $ingredient,
        'form' => $form-,
    ]);
}
```

8. Créer des Fixtures

    1. Installer le bundle DoctrineFixturesBundle

    ```bash
    composer require --dev orm-fixtures
    ```

    2. Créer une classe de fixtures

    ```bash
    symfony console make:fixtures IngredientFixtures
    ```

    3. Charger les fixtures

    ```bash
    symfony console doctrine:fixtures:load
    ```

    4. Installer le bundle Faker

    ```bash
    composer require fakerphp/faker --dev
    ```
