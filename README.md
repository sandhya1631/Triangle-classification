# Triangle-classification
"""
Triangle Classification Module
This module provides functionality to classify triangles based on their side lengths.
"""

def classify_triangle(a, b, c):
    """
    Classify a triangle based on side lengths a, b, c.
    
    Args:
        a, b, c (float or int): The lengths of the triangle sides
        
    Returns:
        str: Classification of the triangle ('equilateral', 'isosceles', 'scalene')
            with 'right' added if it's a right triangle
    """
    # Input validation
    if not (isinstance(a, (int, float)) and isinstance(b, (int, float)) and isinstance(c, (int, float))):
        return 'invalid input'
    
    # Check for positive values
    if a <= 0 or b <= 0 or c <= 0:
        return 'invalid input'
    
    # Sort sides to simplify comparisons
    sides = sorted([a, b, c])
    a, b, c = sides[0], sides[1], sides[2]
    
    # Check triangle inequality theorem
    if a + b <= c:
        return 'not a triangle'
    
    # Check for right triangle (using Pythagorean theorem with small epsilon for float comparison)
    is_right = abs(a*a + b*b - c*c) < 0.001
    
    # Classify based on side lengths
    if abs(a - b) < 0.001 and abs(b - c) < 0.001:
        return 'equilateral' + (' right' if is_right else '')
    elif abs(a - b) < 0.001 or abs(b - c) < 0.001 or abs(a - c) < 0.001:
        return 'isosceles' + (' right' if is_right else '')
    else:
        return 'scalene' + (' right' if is_right else '')

if __name__ == '__main__':
    # Interactive testing
    print("Triangle Classification Program")
    print("Enter the lengths of three sides to classify a triangle.")
    print("Enter 'quit' to exit.")
    
    while True:
        try:
            input_str = input("\nEnter three side lengths (separated by spaces): ")
            if input_str.lower() == 'quit':
                break
                
            sides = [float(x) for x in input_str.split()]
            if len(sides) != 3:
                print("Please enter exactly three numbers.")
                continue
                
            result = classify_triangle(sides[0], sides[1], sides[2])
            print(f"Classification: {result}")
            
        except ValueError:
            print("Invalid input. Please enter numeric values.")
        except Exception as e:
            print(f"An error occurred: {str(e)}")
            
