[![Open in GitHub Codespaces](
  https://img.shields.io/badge/Open%20in%20GitHub%20Codespaces-333?logo=github)](
  https://codespaces.new/dwave-training/iaqom-portfolio-optimization-binary?quickstart=1)
  
# Portfolio Optimization with Stride<sup>TM</sup> Hybrid Solver using Binary Variables 

For the portfolio optimzation problem, we will develop a program that produces an optimized selection of stocks. We will approach this problem using the Stride hybrid solver. We will represent the decision variable as a binary variable.

The objective is to maximimze the total return of the portfolio. The decision variables determine which stocks are included in the portfolio. There are two constraints. First, a certain number of stocks must be selected for the portfolio. Second, the available budget for purchasing stocks is limited.

Using a nonlinear model, we will build the model, then define the objective function and add the constraints. This will return the optimized selection of stocks. 

In this exercise, the average monthly returns and the daily closing prices for 10 stocks are provided. The stocks considered in this exercise are "T" (AT&T), "SFL" (FSL), "PFE" (Pfizer), "XOM" (Exxon Mobil), "MO" (Altria Group), "VZ" (Verizon Communications), "IBM" (IBM), "TSLA" (Tesla), "GILD" (Gilead Sciences), and "GE" (General Electric). 

## Exercise 1

In the first exercise, we will build a basic portfolio of two stocks to maximize the total return and add a constraint for the available budget. The cost of the purchased stocks should be under a certain budget. In this exercise, we will formulate the problem so that it is compatible with the Stride Hybrid solver, but we will not submit it to the solver.  

Open the code file `po_binary_constraints.py`.

   1. Create a nonlinear model object, called `model`, and import the required package.

   2. Add the constants to the model object. 
      - Add `average_returns` to the model object and name it `returns`.
      - Add `num_stocks_to_buy` to the model object and name it `capacity`.
      - Add `daily_prices` to the model object and name it `prices`
      - Add `purchase_budget` to the model object and name it `budget`. 
   
   3. Define the binary decision variable, and store them in `stocks`. Use `len()` to determine the total number of binary variables.

   4. Define the objective function to maximize the total return of the portfolio.

   ```math
   \min \left[-
   {(returns * stocks )}.sum()
   \right]
   ```

   5. Add the constraint to ensure that exactly two stocks are selected. 
   ```math
   stocks.sum() == capacity
   ```

   6. Add the constraint that the cost of the purchased stock should be at most a certain budget. 
   ```math
   {(prices * stocks)}.sum() \leq budget
   ```

## Exercise 2

For exercise 2, we start by creating the model object, add the constants to the model, define the decision binary variable, then set the objective function and add the two constraints, just as we did in exercise 1. 

In this exercise, we will provide an intial state to test the code.

Open the code file `po_binary_initial_state.py`.

   1. Repeat steps 1 to 6 of exercise 1. Copy all the steps that you submitted to the code file `po_binary_constraints.py`. 
   
   2. Lock the model, using a context manager, and proceed with the next steps. 
      
      a. Define the number of states. In this case, only one state is being tested. 
      
      b. Provide the following initial state `[0,0,0,1,1,0,0,0,0,0]`. This is a vector of 10 binary variables that is chosen randomly and satisfies the constraints. Remember to use the `set_state()` method to assign the specifcied state to its index. 
      
      c. Return the initial state for the binary variable symbol, and store it in `stocks_state`. 
      
      d. Return the objective value of the initial state and store it in `objective_value`. 
      
      e. Determine the feasibility status of the initial state, and store it in `model_feasibility`.

## Exercise 3

For exercise 3, we start by creating the model object, add the constants to the model, define the decision binary variable, then set the objective function and add the two constraints, just as we did in exercise 1. 

In this exercise, we will submit the problem to the Stride hybrid solver to obtain an optimal solution.

Open the code file `po_binary_submit.py`.

   1. Repeat steps 1 to 6 of exercise 1. Copy all the steps that you submitted to the code file `po_binary_constraints.py`. 
   
   2. Lock the model explicitly to prevent further changes and to proceed with the next steps. 

   3. Instantiate the nonlinear sampler, and name it `sampler`. Remember to import the required package.
   
   4. Submit the nonlinear model to the nonlinear sampler. Give this problem a label on your Leap dashboard, by using the `label` parameter. Use the label 'Portfolio_Binary'. Note that this label is case sensitive and uses an underscore.

   5. Once you submitted the nonlinear model to the Stride hybrid solver, return the optimal solution for the binary variable symbol, and store it in `stocks_state`. 

   6. Return the objective value of the optimal solution and store it in `objective_value`. 

   7. Determine the feasibility status of the optimal solution, and store it in `model_feasibility`.
