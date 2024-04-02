# DSS_Estrera_Ass.
It shows the Code

import matplotlib.pyplot as plt
import numpy as np
from numpy import sin, cos

# Define the mathematical expressions
expressions = [
    lambda x: x**2 + 7 + 2,
    lambda x: 3*x + 2,
    lambda x: x**2,
    lambda x: x**3,
    lambda x: x**5,
    lambda x: x**3 + 2*x**2 + x + 10,
    lambda x: x**4 - 3*x**3 + 2*x**2 - x + 11,
    lambda x: sin(x),
    lambda x: cos(x),
    lambda x: x**5 + 4*x**4 + x**3 - 2*x**2 + 100
]

# Create a list of x values from 1 to 50
x_values = list(range(1, 51))

# Solve each problem for x values from 1 to 50 and store the results
solutions = [[] for _ in range(10)]
for i, expr in enumerate(expressions):
    for x in x_values:
        solutions[i].append(expr(x))

# Function to plot a graph for a given expression
def plot_graph(expression_number):
    plt.plot(x_values, solutions[expression_number])
    plt.xlabel('x')
    plt.ylabel('Result')
    plt.title(f'Expression {expression_number + 1}')
    plt.show()

# Function to save results to a text file
def save_to_file(expression_number):
    with open('results.txt', 'w') as file:
        file.write(f'x\tResult\n')
        for x, result in zip(x_values, solutions[expression_number]):
            file.write(f'{x}\t{result}\n')

# Function to plot all expressions in one graph
def plot_all_graphs():
    for i, expr in enumerate(expressions):
        plt.plot(x_values, solutions[i], label=f'Expression {i + 1}')
    plt.xlabel('x')
    plt.ylabel('Result')
    plt.title('All Expressions')
    plt.legend()
    plt.show()

# Main program
while True:
    try:
        print("Choose a problem to solve (1-10), or choose 11 to plot all graphs:")
        choice = input()
    except EOFError:
        print("EOFError: Input ended unexpectedly. Please try again.")
        continue

    if choice == "11":
        plot_all_graphs()
        break
    elif choice in map(str, range(1, 11)):
        plot_graph(int(choice) - 1)
        print("Do you want to save the results to a text file? (yes/no)")
        save_choice = input().lower()
        if save_choice == 'yes':
            save_to_file(int(choice) - 1)
    else:
        print("Invalid choice. Please choose a number between 1 and 11.")
