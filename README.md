# online--food--ordering--system
The Online Food Ordering System is a web-based application that allows customers to browse food menus, select their favourite dishes, and place orders online. Users can register, log in, add items to the cart, make payments, and track their orders. Restaurants can manage menus, prices, and customer orders. 
An Online Food Ordering System is a web-based application that allows customers to browse food items, add food to a shopping cart, place orders, and track their orders online. It also provides an admin panel to manage food items, customers, and orders.

Below is a complete academic project guide with project description, objectives, modules, database design, software requirements, and working source code.

I'll use Python Flask, MySQL, HTML, CSS, and Bootstrap for this project because they are suitable for a college-level mini or final-year project.

1. Project abstract
The Online Food Ordering System is designed to simplify the process of ordering food through the internet. Customers can register and log in to the system, view available food items, select their favorite dishes, add items to their cart, and place orders.

The system reduces manual work and saves customers' time. Restaurant administrators can manage food details, update prices, view customer orders, and update order statuses.


{% extends 'base.html' %}

{% block content %}

<div class="hero text-center p-5 mb-4">
    <h1>Delicious Food Delivered To Your Door</h1>
    <p>Order your favourite food online.</p>
</div>

<form method="GET" action="/" class="mb-4">
    <div class="input-group">
        <input type="text" name="search"
               class="form-control"
               placeholder="Search food...">
        <button class="btn btn-success">Search</button>
    </div>
</form>

<h2 class="mb-4">Our Food Menu</h2>

<div class="row">

{% for food in foods %}

<div class="col-md-4 col-lg-3 mb-4">
    <div class="card food-card h-100">

        <img src="{{ food.image or 'https://placehold.co/500x300?text=Food' }}"
             class="card-img-top"
             alt="{{ food.name }}">

        <div class="card-body">

            <h5>{{ food.name }}</h5>

            <p>{{ food.description }}</p>

            <h5 class="text-success">₹{{ food.price }}</h5>

            {% if session.get('user_id') %}
                <form method="POST"
                      action="{{ url_for('add_cart', food_id=food.id) }}">
                    <input type="hidden" name="csrf_token"
                           value="{{ csrf_token() }}">
                    <button class="btn btn-success w-100">
                        Add to Cart
                    </button>
                </form>
            {% else %}
                <a href="/login" class="btn btn-primary w-100">
                    Login to Order
                </a>
            {% endif %}

        </div>
    </div>
</div>

{% else %}
<p>No food items found.</p>
{% endfor %}

</div>

{% endblock %}
