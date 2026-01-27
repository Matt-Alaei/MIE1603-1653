# Column Grouping via MIP

## Problem Definition and Overview
The problem of grouping frequently arises in the context of Structural Engineering. Buildings are made up of many different types of elements, such as beams, walls, slabs, and columns. Taking the example of columns, there can be many thousands of column elements, defined individually at each floor, in a given building. Structural engineers must design these elements based on many conditions such as strength (to ensure the element does not fail under specified loading conditions, such as snow loads), servicability (to ensure there is not excessive vibration or deflection so the residents of the building feel safe), local stability (so the element does not buckle or warp), and global stability (so the entire structure does not collapse). Generally, engineers will choose the smallest section necessary to fulfill those criteria, as larger sections mean higher material costs and higher labour costs in construction. However, desining each element to it's locally optimal section can become incredibly time consuming and lead to challenges with coordination amongst other disciplines who must design around unique element sections at every location. Therefore, there is an incentive to 'group' elements with similar loading and geometric conditions and design every element in the group based on the worst-case in that group. This can becomes a complex optimization problem, which is outside the scope of the typical structural engineer's expertise. Therefore, we look to optimize the grouping of columns in a structural engineering context.

Our contributions in this work is as follows: 
1. we introduce a **MIP** framework for modeling this problem.
2. We investigate the impact of different modifications to the model on solver performance and scalability.

## Methodology
In the literature the most commonly approach to this problem is through heuristics such as **Simulated Annealing**. To our knowledge, there hasn't been an attempt to solve this problem through Operations Research methods such **Mixed Integer Programming (MIP)**. 

In this work, we introduce a novel MIP modeling of the problem and use **_Gurobi_** as our solver. 

## Improvements to The Model
After running our initial model, we made the following tweaks and modifications to our model to improve solver performance and enhance scalability of the model.

These modifications include:
+ **Implicit Continuous Variables:** After running our initial model, we noticed that Gurobi tended some the variables from integer or binary to continuous. As a result, we changed this variables to be continuous in our formulation.
+ **Binary Model:** We also changed some of the constraints so that we coould represent some of the variables as binary variables.
+ **Lazy Constraints:** Lastly, we introduced a lazy callback constraint.

## Experiments
We conducted our experiments on four different building types: **Industrial, Mid-Rise, LTC-Sections,** and **LTC-levels**. To validate our improvements, as part of our ablation studies, we ran 8 variations (we made 3 modifications, which results in $2^3=8$ variations) on each building type; resulting in a total of 32 experiments.

## Results
Through our experiments, we found out that **Binary Model** improvement were the most impactful on **Gap**, improved **Primal** of the model, but consumed more memory. **Continuous Variables** imporvement had the greatest impact on the **Primal** of the model and imporved **Gap** with no seemingly downside. Lastly, **Lazy Constraints** improvement had little impact on **Gap** and slightly worsened **Primal** of the model.

For a more detailed and comprehensive version of our project, see our [report](https://github.com/Matt-Alaei/MIE1603-1653/blob/main/MIE1603-1653-Group4-Report.ipynb).