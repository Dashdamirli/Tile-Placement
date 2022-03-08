# Tile-Placement

The tile placement problem requires us to place the el,outer or full block shaped 4x4 tiles on a square which contains bushes, marked by colors: 1, 2, 3, 4. 

First thing we have to define is our variables, their domains and constraints we have to enforce on those variables. Instead of looking at the landscape one bush at a time, we will look at it as a list of 4x4 squares to make it easier to assign tiles to them. So, our variables will be those squares for which we have to assign values which are the appropriate tile shapes. 

We will have two types of constraints: 
<ul>
  <li>Number of tile shapes we have placed should not exceed available tiles
  <li>Number of visible bushes by color should not exceed given targets
<ul>
  
Instead of calculating how many bushes there are for each color and then subtracting from respective counts as we ‘cover’ bushes, I decided to initially assign zero to each colored bush and add visible bush count as the tiles are placed. 

Now we have to decide in which order we will traverse the landscape. Does that even matter? Turns out it does. At first, I tried going in order but it solved one of the input files in approximately 35 seconds. Not bad, but the landscape here is only 20x20, so it needed improvement. Then I decided to sort squares by the number of visible bushes they contain in descending order. By doing that we allow faster convergence, therefore faster execution. This method solved that same problem in under 3 seconds which is more than 10 times faster.

The biggest problem with this project was the constraint propagation. Any tile that has been placed on one square does not affect the tile that can be placed on the next square. We could remove some tile shapes from other squares’ domains if they would exceed the target bush color count but that would bring us to unnecessary complexity because we already check for any constraint violation before doing anything and our domain is not big.
