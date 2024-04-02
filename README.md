# DSS_Estrera_Ass.
It shows the Graph and Files

import matplotlib.pyplot as plt
import random

def solve_expression(x_values, expression):
    y_values = [max(0, expression(x)) for x in x_values]
    return y_values

def write_to_file(x_values, y_values_dict):
    with open("graph_numbers.txt", "w") as file:
        for i, (expression_name, values) in enumerate(y_values_dict.items(), start=1):
            file.write(str(i) + ". " + expression_name + ":\n")
            file.write(", ".join(map(str, values)))  # Join values with comma
            file.write("\n" * 11)  # Add 11 newlines

def plot_expression(x_values, y_values, expression_name):
    plt.figure(figsize=(12, 8))
    plt.plot(x_values, y_values, label=expression_name, linewidth=2)
    
    plt.title(f"Graph of {expression_name}")
    plt.xlabel('x')
    plt.ylabel('y')
    plt.xlim(left=0)
    plt.ylim(bottom=0)
    plt.legend(loc='upper left')
    plt.grid(True)
    plt.show()

def solve_and_graph_specific_problem(input_file, output_file, problem_number):
    try:
        with open(input_file, 'r', encoding='utf-8') as input_f:
            expressions = input_f.readlines()

            # Extract the expression for the specified problem number
            expr_str = expressions[problem_number - 1].strip()

            # Define the expression as a lambda function
            expr = eval(f"lambda x: {expr_str}")

            # Generate random x values from 1 to 50
            x_values = [random.randint(1, 50) for _ in range(50)]
            
            # Evaluate the expression for each x value
            y_values = [expr(x_val) for x_val in x_values]

            # Plot the graph
            plt.plot(x_values, y_values)
            plt.title(f"Graph of Problem {problem_number}")
            plt.xlabel('x')
            plt.ylabel('y')
            plt.grid(True)
            plt.show()

            # Write solutions to the output file
            with open(output_file, 'w', encoding='utf-8') as output_f:
                output_f.write(f"Solutions for Problem {problem_number}:\n")
                for x_val, y_val in zip(x_values, y_values):
                    output_f.write(f"x = {x_val}, y = {y_val}\n")

    except FileNotFoundError:
        print("Input file not found.")
    except Exception as e:
        print("An error occurred:", str(e))
        return

# Example usage:
input_file = 'values.txt'  # Replace 'values.txt' with your input file
output_file = 'graph_numbers.txt'  # Specify the output file path

print('Choose a Problem:')
print('1. x² + 7x +2') 
print('2. 3x + 2')
print('3. x²')
print('4. x³')
print('5. x⁵')
print('6. x³ + 2x² + x + 10')
print('7. x⁴ -3x³ + 2x² - x + 11')
print('8. Sin(x)')
print('9. Cos(x)')
print('10. 4x⁴ + x³ - 2x² + 100')
print()

try:
    problem_number = int(input("Enter the problem number to be solved and graphed: "))
    solve_and_graph_specific_problem(input_file, output_file, problem_number)
except ValueError:
    print("Invalid input. Please enter a number.")
