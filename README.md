# gittest
<div>
  <h2>Add Ingredients to Meal</h2>

  <!-- Search for ingredients -->
  <label for="ingredient-search">Search for an ingredient</label>
  <input type="text" id="ingredient-search" [(ngModel)]="searchTerm" (input)="searchIngredients()">
  
  <!-- Display search results -->
  <ul *ngIf="searchResults.length > 0">
    <li *ngFor="let ingredient of searchResults">
      {{ ingredient.ingredientName }} 
      <button (click)="addIngredient(ingredient)">Add</button>
    </li>
  </ul>

  <!-- List of selected ingredients -->
  <h3>Selected Ingredients</h3>
  <table>
    <thead>
      <tr>
        <th>Ingredient Name</th>
        <th>Quantity</th>
        <th>Action</th>
      </tr>
    </thead>
    <tbody>
      <tr *ngFor="let ingredient of selectedIngredients">
        <td>{{ ingredient.ingredientName }}</td>
        <td>
          <input type="number" [(ngModel)]="ingredient.quantity">
        </td>
        <td>
          <button (click)="removeIngredient(ingredient)">Remove</button>
        </td>
      </tr>
    </tbody>
  </table>

  <!-- Button to finalize meal -->
  <button (click)="finalizeMeal()">Save Meal</button>
</div>
import { Component, OnInit } from '@angular/core';
import { Ingredient } from './ingredient.model'; // Your ingredient model
import { MealsService } from './meals.service'; // Your service to fetch ingredients

@Component({
  selector: 'app-meal',
  templateUrl: './meal.component.html',
  styleUrls: ['./meal.component.css']
})
export class MealComponent implements OnInit {
  searchTerm: string = '';
  searchResults: Ingredient[] = []; // Search result from the database
  selectedIngredients: { ingredientName: string, ingredientId: number, quantity: number }[] = []; // Ingredients added to the meal

  constructor(private mealsService: MealsService) {}

  ngOnInit(): void {
    // You can load initial data if needed
  }

  // Search for ingredients based on the user's input
  searchIngredients() {
    if (this.searchTerm.trim() === '') {
      this.searchResults = [];
      return;
    }

    this.mealsService.searchIngredients(this.searchTerm).subscribe((results: Ingredient[]) => {
      this.searchResults = results;
    });
  }

  // Add an ingredient to the selected list
  addIngredient(ingredient: Ingredient) {
    this.selectedIngredients.push({
      ingredientId: ingredient.ingredientId,
      ingredientName: ingredient.ingredientName,
      quantity: 1 // Default quantity
    });

    // Clear search
    this.searchResults = [];
    this.searchTerm = '';
  }

  // Remove an ingredient from the list
  removeIngredient(ingredient: any) {
    this.selectedIngredients = this.selectedIngredients.filter(i => i.ingredientId !== ingredient.ingredientId);
  }

  // Finalize the meal and send it to the backend
  finalizeMeal() {
    // Here you can send selectedIngredients to the backend
    console.log('Meal with ingredients', this.selectedIngredients);

    // Save meal using a service or API call
    // mealsService.saveMeal(selectedIngredients).subscribe(...)
  }
}

searchIngredients(term: string): Observable<Ingredient[]> {
  return this.http.get<Ingredient[]>(`${this.baseUrl}/ingredients/search?name=${term}`);
}


@GetMapping("/ingredients/search")
public List<Ingredient> searchIngredients(@RequestParam String name) {
    return ingredientService.searchByName(name); // Implement search logic in service
}


/* Styling for the Add Ingredients section */
.add-ingredients-container {
  margin: 20px 0;
  padding: 20px;
  border: 1px solid #ccc;
  border-radius: 8px;
  background-color: #f9f9f9;
  max-width: 600px;
}

.add-ingredients-container h2 {
  margin-bottom: 20px;
  font-size: 24px;
  color: #333;
}

.add-ingredients-container label {
  font-size: 16px;
  margin-right: 10px;
}

.add-ingredients-container input {
  padding: 8px;
  font-size: 16px;
  border: 1px solid #ccc;
  border-radius: 4px;
  margin-right: 10px;
}

.add-ingredients-container button {
  padding: 8px 12px;
  background-color: #007bff;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

.add-ingredients-container button:hover {
  background-color: #0056b3;
}

/* Styling for the ingredients list */
.ingredient-list {
  list-style-type: none;
  padding: 0;
  margin-top: 20px;
}

.ingredient-list li {
  display: flex;
  justify-content: space-between;
  margin-bottom: 10px;
  padding: 8px;
  border-bottom: 1px solid #ddd;
}

.ingredient-list li button {
  background-color: #28a745;
  color: white;
  padding: 4px 8px;
  border: none;
  border-radius: 4px;
}

.ingredient-list li button:hover {
  background-color: #218838;
}

/* Styling for the selected ingredients table */
.table-container {
  margin-top: 20px;
}

.table-container table {
  width: 100%;
  border-collapse: collapse;
  margin-top: 20px;
}

.table-container th,
.table-container td {
  padding: 12px;
  text-align: left;
  border-bottom: 1px solid #ddd;
}

.table-container th {
  background-color: #f2f2f2;
  font-size: 18px;
}

.table-container td input {
  width: 60px;
  padding: 5px;
}

.table-container td button {
  padding: 5px 10px;
  background-color: #dc3545;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

.table-container td button:hover {
  background-color: #c82333;
}

/* Save button styling */
.save-button {
  margin-top: 20px;
  padding: 10px 20px;
  background-color: #007bff;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

.save-button:hover {
  background-color: #0056b3;
}

/* Responsive design */
@media (max-width: 768px) {
  .add-ingredients-container,
  .table-container {
    width: 100%;
  }

  .ingredient-list li {
    flex-direction: column;
    align-items: flex-start;
  }

  .ingredient-list li button {
    margin-top: 5px;
  }
}
