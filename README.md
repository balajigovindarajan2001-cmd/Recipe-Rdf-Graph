# Recipe-Company RDF Graph

**EXPLANATION – Vinzent Aschir and Balaji Govindarajan**

## Getting the Project
Clone the repository using Git:

```bash
git pull https://github.com/balajigovindarajan2001-cmd/Recipe-Rdf-Graph
```

## Recipe Level – Vinzent

We implemented a `Recipe` class with nine properties, four of which store general information as strings. Each recipe is assigned a unique **ID** (string) to distinguish between different recipes for the same dish.

### Cuisine
Gastronomies are represented by subclasses of `Cuisine`, such as `ItalianCuisine`. Recipes or menus are linked to the appropriate cuisine using the `hasCuisine` property.

### Health
To account for health concerns, we created instances of the `Allergen` class (e.g., `Gluten`) and linked them to recipes or ingredients using a dedicated property to indicate potential allergic reactions. Recipes can also be categorized as `Vegan` or `Vegetarian` by making them instances of these subclasses.

### Course Classification
The class `Courses` (another subclass of `Recipe`) organizes recipes into different courses. Recipes can be instances of:

- `MainDish`
- `Appetizer`
- `Dessert`

### Time
Durations are represented using **ISO 8601 duration format**, allowing for flexible specification of periods ranging from a few minutes to multiple days. This approach also facilitates integration with external ontologies, such as Schema.org.

### Ingredients
To provide a machine-readable ingredient list and avoid duplication, recipes are linked to an `IngredientBundle` instance via the `hasIngredientList` property. Each bundle contains triples representing:

- The **ingredient**  
- Its **amount** (decimal)  
- The **unit**  

Both amount and unit are optional; for example, spices like sugar may not have a quantity or unit and are included only for flavor.

#### Subclasses of Ingredients
Ingredients have subclasses specifying their type, such as `Spice` or `Drink`. These subclasses can be linked to allergens (e.g., `DairyProduct` linked to `MilkAllergy`). The property indicating an allergen is inherited by `Ingredient`. Instead of using `rdf:label`, we use `rbox:hasName` to assign names to `Ingredient` instances.

#### Units
The `Unit` class has several subclasses, such as `VolumeUnit` or `CountUnit`. Specific units (e.g., grams, inches) are instances of these subclasses.

### Menu
Different recipes can be grouped together within an instance of the `Menu` class. For demonstration, we created instances representing **German**, **French**, and **Italian** menus. Each menu instance uses the same core identifying and descriptive attributes as individual recipes, such as `hasID` and `hasDescription`.

### Coding
All class definitions at the recipe level are labeled and commented in **German and English**. Some instances and properties are also labeled; however, full labeling and commenting were omitted due to time constraints.  

- **Visualization:** GraphDB Demo Version  
- **Assistance:** ChatGPT, GitHub Copilot, Google, and other search engines for debugging and coding  
- **Implementation:** The RDF graph design, ontology decisions, and overall implementation were performed independently by the team  

**Total triples:** 1,643

---

## Company Level – Balaji

### How It Works
Customers subscribe to a **SubscriptionPlan**. After selecting one of the available subscription plans, an included menu is chosen. The recipes that belong to the selected menu are then ordered via an **OrderLine**.

---

### Subscription Plan
Subscriptions are divided into categories such as **3 recipes × 2 people** or **4 recipes × 4 people**. Based on customer requirements, an appropriate plan is selected.

An instance of the class **SubscriptionPlan** holds the following properties to support popularity evaluation and decision-making:
- `planOrderCount`
- `planReviewCount`
- `planAverageRating`
- `planPopularityScore`

Using these popularity-related metrics, customers can compare and choose a suitable plan.

---

### Order
An instance of the class **Order** holds one or more **OrderLine** instances via the property `hasOrderLine`.

An **OrderLine**, belonging to a specific order, summarizes for the customer all ordered recipes, whether they originate from different menus or from individually selected recipes.

---

### Courier
An instance **DeliveryPerson** of the class **Courier** has a customer-provided rating (string).

The attributes `deliveryStart` and `deliveryEnd` indicate whether a delivery is delayed. A **Courier** instance also contains properties describing customer details and the delivery destination.

---

### Review
A **Review** consists of:
- a **review body**, containing the textual review (string)
- **review ratings**, represented as an integer

Based on the reviews, a popularity score is calculated.

For properties with integer, string, or other literal ranges, `rdfs:DatatypeProperty` was used instead of `rdf:Property`.

---

## Coding
All class definitions at the recipe level are labeled and commented in both German and English. Some instances and properties are also labeled; however, full labeling and commenting were omitted due to time constraints.

**GraphDB (Demo Version)** was used for visualization.

The following tools were used to assist with debugging and coding:
- ChatGPT
- GitHub Copilot
- Google and other search engines

The design of the RDF graph, ontology decisions, and overall implementation were carried out independently by the team.

---

**Total number of triples:** 1643
