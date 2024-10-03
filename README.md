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
