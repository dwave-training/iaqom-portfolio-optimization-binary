[![Open in GitHub Codespaces](
  https://img.shields.io/badge/Open%20in%20GitHub%20Codespaces-333?logo=github)](
  https://codespaces.new/dwave-training/iaqom-portfolio-optimization-binary?quickstart=1)
  
# Portfolio Optimization With The Stride<sup>TM</sup> Hybrid Solver Using Binary Variables 

For the portfolio optimization problem, convert the mathematical formulation into a model in Python code. Use binary variables to represent the decision variable and code the problem so that it is compatible for submission to the Stride hybrid solver.

The objective is to maximize the total return of the portfolio. The decision variable represents the stocks that are included in the portfolio. There are two constraints: a certain number of stocks must be selected for the portfolio, and the available budget for purchasing stocks cannot be exceeded.

Build the nonlinear model, define the objective function, and add the constraints.

In this exercise, the average monthly returns and the daily closing prices for 10 stocks are provided. The stocks considered in this exercise are "T" (AT&T), "SFL" (FSL), "PFE" (Pfizer), "XOM" (Exxon Mobil), "MO" (Altria Group), "VZ" (Verizon Communications), "IBM" (IBM), "TSLA" (Tesla), "GILD" (Gilead Sciences), and "GE" (General Electric).

## Exercise 1

In the first exercise, build a basic portfolio of two stocks to maximize the total return. Add a constraint that the cost of the purchased stocks cannot exceed a certain budget. Formulate the problem so that it is compatible for submission to the Stride Hybrid solver, but do not yet submit it to the solver.

Open `po_binary_constraints.py`.

   1. Import the relevant package(s).

   2. Create a nonlinear model object called `model`.

   3. Add the following constants to the model object:
      - `average_returns` and name it `returns`.
      - `num_stocks_to_buy` and name it `capacity`.
      - `daily_prices` and name it `prices`.
      - `purchase_budget` and name it `budget`.
   
   4. Define the binary decision variable and store it in `stocks`. Use `len` to determine the total number of binary variables.

   5. Define the following objective function to maximize the total return of the portfolio:

   ```math
   \min \left[-
   {(returns * stocks )}.sum()
   \right]
   ```

   6. Add the constraint to ensure that exactly two stocks are selected.
   ```math
   stocks.sum() == capacity
   ```

   7. Add the constraint that the cost of the purchased stocks cannot exceed a certain budget.
   ```math
   {(prices * stocks)}.sum() \leq budget
   ```

## Exercise 2

For exercise 2, provide an initial state to test the code.

Start with the work completed in exercise 1. Create the model object, add the constants to the model, define the decision variable, set the objective function, and add the two constraints. Then, provide an initial state.


Modify `po_binary_initial_state.py` as follows:

   1. Repeat steps 1 to 7 of exercise 1. You may copy all the work you submitted in `po_binary_constraints.py`.
   
   2. Lock the model using a context manager and include the following steps in the block:
      
      a. Define the number of states. In this case, only one state is being tested.
      
      b. Provide the following initial state `[0, 0, 0, 1, 1, 0, 0, 0, 0, 0]`, a vector of 10 binary variables. The vector is chosen randomly and satisfies the constraints. Remember to use the `set_state` method to assign the specified state to its index.
      
      c. Return the initial state for the binary variable symbol and store it in `stocks_state`.
      
      d. Return the objective value of the initial state and store it in `objective_value`.
      
      e. Determine the feasibility status of the initial state and store it in `model_feasibility`.

## Exercise 3

For exercise 3, submit the problem to the Stride hybrid solver to obtain the best solution.

Start with the work completed in exercise 1. Create the model object, add the constants to the model, define the decision variable, set the objective function, and add the two constraints. Then, submit the problem to the Stride solver.


Open `po_binary_submit.py`.

   1. Repeat steps 1 to 7 of exercise 1. You may copy all the work you submitted in `po_binary_constraints.py`.
   
   2. Lock the model explicitly to prevent further changes.

   3. Instantiate the nonlinear sampler and name it `sampler`.
   
   4. Submit the nonlinear model to the Stride hybrid solver. Label your problem "Portfolio_Binary" using the `label` parameter. The label is case-sensitive and uses an underscore. When you submit your problem, the label displays on your Leap dashboard.

   5. Return the best solution for the binary variable symbol and store it in `stocks_state`.

   6. Return the best solution's objective value and store it in `objective_value`.

   7. Determine the best solution's feasibility status and store it in `model_feasibility`.