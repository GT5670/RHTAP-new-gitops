from flask import Flask, jsonify, request
from flasgger import Swagger
app = Flask(__name__)
swagger = Swagger(app)
products = [
    {"id": 1, "name": "laptop", "price": 1200},
    {"id": 2, "name": "mouse", "price": 1200},
    {"id": 3, "name": "keyboard", "price": 1200}
]
@app.route('/')
def home():
    """
    Home route
    ---
    responses:
        200:
            description: Welcome message
    """
    return jsonify({"message": "Welcome to the API"}), 200
@app.route('/products', methods=['GET'])
def get_products():
    """
    Get all products
    ---
    parameters:
      - name: product
        in: body
        required: true
        schema:
          type: object
          properties:
            name:
              type: string
            price:
              type: integer
    response:
      200:
        description: This is a list of products.
    """
    return jsonify(products), 200
@app.route('/products', methods=['POST'])
def add_product():
    """
    Create a product
    ---
    parameters:
      - name: product
        in: body
        required: true
        schema:
          type: object
          properties:
            name:
              type: string
            price:
              type: integer
    response:
      200:
        description: This is a list of products.
      400:
        description: Invalid product
    """
    data = request.get_json()
    if not data or "name" not in data or "price" not in data:
        return jsonify({"error": "Invalid response"}), 400
    new_product = {"id": len(products)+1, "name": data["name"], "price": data["price"]}
    products.append(new_product)
    return jsonify(new_product), 200
if __name__ == '__main__':
    app.run(debug=True)
