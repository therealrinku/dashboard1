# dashboard

## Summary
vue js app

## Project Structure
Pages:App.vue
Components:Table.vue and Select.vue
data:enquiries.json


## Components Grouping

I have added two components which are Table.vue and Select.vue because I wanted to have seperate component for Table for better structure and I have created Select.vue to be able to reuse it without repeating same code multiple times.

And there is App.vue which is the homepage.


## Functionality
Sorting and Filtering:I have done all the sorting and filtering functionalities inside the Table.vue by using props passed from App.vue to make it simpler with as much less code possible(in my view)

Pagination: I have added two buttons which updates pageNo value and used watch method whenever the pageNo value in the state changes to run a function which uses slice method to update the enquiries array.
