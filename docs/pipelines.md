<header class="pf-v5-c-masthead pf-m-display-stack pf-m-display-inline-on-lg"
  id="primary-detail-expanded-example-masthead">
  <span class="pf-v5-c-masthead__toggle" id="masthead-toggle">
    <button class="pf-v5-c-button pf-m-plain" type="button" aria-label="Global navigation">
      <i class="fas fa-bars" aria-hidden="true"></i>
    </button>
  </span>

  <div class="pf-v5-c-masthead__main">
    <a class="pf-v5-c-masthead__brand" href="{{ url_for('home') }}">
      <img class="pf-v5-c-brand" src="{{ url_for('static', filename='images/red-hat-logo.svg') }}" alt="Red Hat logo"
        style="--pf-v5-c-brand--Height:36px" />
    </a>
  </div>
  <div class="pf-v5-c-masthead__content">
    <div class="pf-v5-c-toolbar pf-m-full-height pf-m-static" id="primary-detail-expanded-example-masthead-toolbar">
      <div class="pf-v5-c-toolbar__content">
        <div class="pf-v5-c-toolbar__content-section">
          <div
            class="pf-v5-c-toolbar__group pf-m-icon-button-group pf-m-align-right pf-m-spacer-none pf-m-spacer-md-on-md pf-m-hidden pf-m-visible-on-lg"
            style="position: relative;">
            <div class="search-bar-container pf-v5-c-search-input" id="search-bar">
              <div class="pf-v5-c-input-group">
                <span class="pf-v5-c-search-input__icon">
                  <i class="fas fa-search fa-fw" aria-hidden="true"></i>
                </span>
                <input class="pf-v5-c-search-input__text-input" type="text" placeholder="Search products"
                  aria-label="Search products" id="search-input" />
              </div>
            </div>
            <button class="pf-v5-c-button pf-m-control search-arrow" type="submit" aria-label="Search"
              onclick="submitSearch()">
              <i class="fas fa-arrow-right" aria-hidden="true"></i>
            </button>
            <ul class="search-results" id="search-results"></ul>
          </div>
          <div class="pf-v5-c-toolbar__item pf-m-hidden pf-m-visible-on-sm">
            {% if "anonymous" in needs.type %}
            <a class="pf-v5-c-button pf-m-primary pf-m-small" href="/saml/sso">
              <span class="pf-v5-c-menu-toggle__text">Login</span>
            </a>
            {% elif "authenticated" in needs.type %}
            <button class="pf-v5-c-menu-toggle pf-m-full-height" type="button" aria-expanded="false">
              <span class="pf-v5-c-menu-toggle__text">Welcome, {{ user }}</span> &nbsp;&nbsp;&nbsp;&nbsp;
              <a class="pf-v5-c-button pf-m-primary pf-m-small" href="/saml/logout">
                <span class="pf-v5-c-menu-toggle__text">Logout</span>
              </a>
            </button>
            {% endif %}
          </div>
        </div>
      </div>
    </div>
  </div>
</header>
<script src="{{ url_for('static', filename='scripts/search.js') }}"></script>




document.addEventListener('click', function(event) {
  const searchBar = document.getElementById('search-bar');
  const searchResults = document.getElementById('search-results');
  const searchArrow = document.querySelector('.search-arrow');

  // Check if the click is outside the search bar, search results, and search arrow
  if (!searchBar.contains(event.target) && !searchResults.contains(event.target) && !searchArrow.contains(event.target)) {
    searchResults.style.display = 'none';
  }
});

document.getElementById('search-input').addEventListener('input', function() {
  const query = this.value;
  const searchResults = document.getElementById('search-results');

  if (query.length < 2) {
    searchResults.style.display = 'none';
    return;
  }

  fetch(`/opl/ajax-search?q=${query}`)
    .then(response => response.json())
    .then(data => {
      searchResults.innerHTML = '';
      if (data.length > 0) {
        searchResults.style.display = 'block';
        data.forEach(product => {
          const li = document.createElement('li');
          li.textContent = product.name;
          li.addEventListener('click', function() {
            window.location.href = `/opl/product/${product.id}`;
          });
          searchResults.appendChild(li);
        });
      } else {
        searchResults.style.display = 'none';
      }
    });
});

function submitSearch() {
  const query = document.getElementById('search-input').value;
  if (query.length > 0) {
    window.location.href = `/opl/search-to-view-products?product_name=${encodeURIComponent(query)}`;
  }
}



{% extends 'base.html' %}

{% block heading %}
<h2 class="pf-v5-c-title pf-m-xl">Search products</h2>
{% endblock %}

{% block content %}
<script>
    function resetForm() {
        window.location.href = "{{ url_for('view_routes.reset_search_form') }}";
    }
</script>
<div class="pf-v5-c-page__main-section">
    <!-- Section 1: Search -->
    <fieldset class="pf-v5-c-form pf-m-horizontal">
        <legend class="pf-v5-c-title">Search by</legend>
        <form method="post" action="{{ url_for('view_routes.view_products') }}">
            {{ form.csrf_token }}
            {{ form.hidden_tag() }}

            <div class="pf-v5-c-form__group">
                <label class="pf-v5-c-form__label" for="product_name">
                    <span class="pf-v5-c-form__label-text">Product name</span>
                </label>
                {{ form.product_name(class="pf-v5-c-form-control", value=request.args.get('product_name', '')) }}
            </div>

            <div class="pf-v5-c-form__group">
                <label class="pf-v5-c-form__label" for="product_status">
                    <span class="pf-v5-c-form__label-text">Product status</span>
                </label>
                {{ form.product_status(class="pf-v5-c-form-control") }}
            </div>

            <div class="pf-v5-c-form__group">
                <label class="pf-v5-c-form__label" for="product_type">
                    <span class="pf-v5-c-form__label-text">Product type</span>
                </label>
                {{ form.product_type(class="pf-v5-c-form-control") }}
            </div>

            <div class="pf-v5-c-form__actions">
                {{ form.submit(class="pf-v5-c-button pf-m-primary") }}
                <button type="button" class="pf-v5-c-button pf-m-secondary" onclick="resetForm()">Reset</button>
        </form>
</div>
</fieldset>

<!-- Section 2: Search Results -->
{% if form.is_submitted() and form.validate() %}
<fieldset class="pf-v5-c-form">
    <legend class="pf-v5-c-title">Search results</legend>
    <div class="pf-v5-c-content">
        {% if products_with_portfolios %}
        <ul class="pf-v5-c-list">
            {% for product in products_with_portfolios %}
            <li class="pf-v5-c-list__item">
                <div class="pf-v5-c-content">
                    <p class="pf-v5-c-title">
                        <a href="{{ url_for('view_routes.view_product_details', product_id=product.product_id) }}">
                            {{ product.product_name }}
                        </a>
                    </p>
                    <p><strong>Status:</strong> {{ product.product_status }}</p>
                    <p><strong>Last Updated:</strong> {{ product.last_updated.strftime('%d %B %Y') }}</p>
                    {% if product.portfolio_names and product.portfolio_names|select('!=', None)|list|length > 0 %}
                    <p><strong>Portfolios:</strong> {{ product.portfolio_names|join(', ') }}</p>
                    {% endif %}
                    <p><strong>Product Types:</strong> {{ ', '.join(product.product_types) }}</p>
                </div>
            </li>
            {% endfor %}
        </ul>
        {% else %}
        <p>No results found.</p>
        {% endif %}
    </div>
</fieldset>
{% endif %}
</div>
{% endblock %}


from flask import Blueprint, render_template, request, jsonify, current_app, session as flask_session, flash, redirect, url_for
from models import Product
from sqlalchemy import or_, func
from forms import MyForm, SearchForm, EditForm
from models import db, Product, ProductType, ProductTypeMap, ProductPortfolios, ProductPortfolioMap, ProductNotes, ProductReferences, ProductAlias, ProductMktLife, ProductPartners, Partner, ProductComponents, ProductLog
from sqlalchemy.exc import OperationalError, ProgrammingError
import time
import logging
import os
from flask import g
import permissions
from sqlalchemy import or_

# Configure logging
logging.basicConfig(level=logging.DEBUG)
logger = logging.getLogger(__name__)

# Environment variables for retry logic
RETRY_ATTEMPTS = int(os.getenv('RETRY_ATTEMPTS', 5))
RETRY_WAIT_TIME = int(os.getenv('RETRY_WAIT_TIME', 2))
SERIALIZABLE_ERROR_CODE = 'XX000'
view_routes = Blueprint('view_routes', __name__)

def retry_db_operation(operation, attempts=RETRY_ATTEMPTS, wait_time=RETRY_WAIT_TIME):
    for attempt in range(attempts):
        try:
            return operation()
        except (OperationalError, ProgrammingError) as e:
            if isinstance(e, ProgrammingError) and e.orig.pgcode != SERIALIZABLE_ERROR_CODE:
                raise
            logger.error(f"Attempt {attempt + 1} failed with error: {e}")
            time.sleep(wait_time * (2 ** attempt))  # Exponential backoff
    logger.error(f"All attempts to perform the operation failed after {attempts} attempts.")
    raise Exception("Database operation failed after multiple attempts.")

@view_routes.route('/opl/search-to-view-products', methods=['GET', 'POST'])
def view_products():
    # Initialize variables
    form = SearchForm()
    products = []
    products_with_portfolios = []
    selected_product = None  # Initialize to avoid UnboundLocalError

    session = current_app.config['Session']()
    try:
        # Define the base query
        products_query = session.query(
            Product.product_id.label('product_id'),
            Product.product_name.label('product_name'),
            Product.product_status.label('product_status'),
            Product.last_updated.label('last_updated'),
            ProductPortfolios.category_name.label('category_name'),
            ProductType.product_type.label('product_type'),
            Product.is_admin_only.label('is_admin_only')  # Include and label
        ).outerjoin(ProductPortfolioMap, Product.product_id == ProductPortfolioMap.product_id)\
         .outerjoin(ProductPortfolios, ProductPortfolioMap.category_id == ProductPortfolios.category_id)\
         .join(ProductTypeMap, ProductTypeMap.product_id == Product.product_id)\
         .join(ProductType, ProductType.type_id == ProductTypeMap.type_id)\
         .outerjoin(ProductAlias, ProductAlias.product_id == Product.product_id)\
         .order_by(Product.product_name)

        # Check user permissions
        user_is_admin = permissions.opl_editor_permission.can()
        logger.debug(f"user_is_admin: {user_is_admin}")

        if not user_is_admin:
            products_query = products_query.filter(
                or_(
                    Product.is_admin_only == False,
                    Product.is_admin_only.is_(None)
                )
            )

        # Handle search parameters from GET or POST request
        search_query = None
        product_status = None
        product_type = None

        if request.method == 'POST' and form.validate_on_submit():
            # Handle form submission
            search_query = form.product_name.data
            product_status = form.product_status.data
            product_type = form.product_type.data
        else:
            # Handle search query from GET request
            search_query = request.args.get('product_name', '')
            form.product_name.data = search_query  # Set the form field

        # Apply search filters
        if search_query:
            search_term = f"%{search_query}%"
            products_query = products_query.filter(
                or_(
                    Product.product_name.ilike(search_term),
                    ProductAlias.alias_name.ilike(search_term)
                )
            )
        if product_status and product_status != 'Select':
            products_query = products_query.filter(Product.product_status == product_status)
        if product_type:
            type_id = product_type
            if isinstance(type_id, list):
                type_id = type_id[0]
            products_query = products_query.filter(ProductType.type_id == type_id)

        # Fetch products
        products = products_query.all()

        # Process results
        product_dict = {}
        for product in products:
            product_id = product.product_id
            if product_id not in product_dict:
                product_dict[product_id] = {
                    'product_id': product.product_id,
                    'product_name': product.product_name,
                    'product_status': product.product_status,
                    'last_updated': product.last_updated,
                    'portfolio_names': set(),
                    'product_types': set(),
                    'is_admin_only': product.is_admin_only
                }
            if product.category_name:
                product_dict[product_id]['portfolio_names'].add(product.category_name)
            if product.product_type:
                product_dict[product_id]['product_types'].add(product.product_type)

        # Convert to list
        products_with_portfolios = [
            {
                'product_id': prod['product_id'],
                'product_name': prod['product_name'],
                'product_status': prod['product_status'],
                'last_updated': prod['last_updated'],
                'portfolio_names': sorted(prod['portfolio_names']),
                'product_types': sorted(prod['product_types']),
                'is_admin_only': prod['is_admin_only']
            }
            for prod in product_dict.values()
        ]

    except Exception as e:
        logger.error(f"Error during product retrieval: {e}")
        flash('An error occurred while retrieving products.', 'error')
    finally:
        session.close()

    # Render template
    return render_template(
        'opl/view_search.html',
        form=form,
        products_with_portfolios=products_with_portfolios,
        user_is_admin=user_is_admin
    )


# Flask route for resetting the form
@view_routes.route('/reset-view-search-form', methods=['GET'])
def reset_search_form():
    form = SearchForm()  # Creates a new form instance with default values
    return render_template('opl/view_search.html', form=form)


@view_routes.route('/opl/ajax-search', methods=['GET'])
def ajax_search():
    search_term = request.args.get('q', '')
    if not search_term:
        return jsonify([])

    search_term = f"%{search_term}%"
    products = retry_db_operation(lambda: Product.query.outerjoin(ProductAlias).filter(
        or_(Product.product_name.ilike(search_term),
            ProductAlias.alias_name.ilike(search_term))
    ).all())

    results = []
    for product in products:
        results.append({
            'id': product.product_id,
            'name': product.product_name
        })

    return jsonify(results)

# Route to view detailed information for a specific product
@view_routes.route('/opl/product/<string:product_id>', methods=['GET'])
def view_product_details(product_id):
    # Retrieve the product based on the provided product_id
    product = retry_db_operation(lambda: Product.query.get_or_404(product_id))

    if not product:
        # Handle the case where the product is not found
        return render_template('opl/view.html', product=None)

    # Fetch the associated product types
    product_types = retry_db_operation(lambda: ProductType.query.join(ProductTypeMap).filter_by(product_id=product_id).all())

    # Fetch the associated product portfolios
    product_portfolios = retry_db_operation(lambda: ProductPortfolioMap.query.filter_by(product_id=product_id).all())

    # Extract category_ids from the portfolio mappings
    category_ids = [portfolio.category_id for portfolio in product_portfolios]

    # Fetch the actual portfolios based on the category_ids
    portfolios = retry_db_operation(lambda: ProductPortfolios.query.filter(ProductPortfolios.category_id.in_(category_ids)).all())

    # Get partner choices
    partner_choices = retry_db_operation(lambda: [(partner.partner_id, partner.partner_name) for partner in Partner.query.all()])

    # Get component choices
    component_choices = [('', 'Select')] + retry_db_operation(lambda: [(component.product_id, component.product_name) for component in Product.query.all()])

    # Get product notes
    product_notes = retry_db_operation(lambda: ProductNotes.query.filter_by(product_id=product_id).first())

    # Fetch the associated product references
    product_references = product.product_references

    # Fetch the associated product aliases
    product_aliases = product.aliases

    # Fetch the associated product release information
    product_mkt_life = retry_db_operation(lambda: ProductMktLife.query.filter_by(product_id=product_id).first())

    # Fetch the associated product partners
    product_partners = retry_db_operation(lambda: ProductPartners.query.filter_by(product_id=product_id).all())

    # Retrieve the parent and child components
    product_components = retry_db_operation(lambda: ProductComponents.query.filter_by(component_id=product_id).all())
    child_components = retry_db_operation(lambda: ProductComponents.query.filter_by(product_id=product_id).all())

    # Create dictionaries to store component names for sorting
    component_product_names = {comp.product_id: Product.query.get(comp.product_id).product_name for comp in product_components}
    component_product_name = {comp.component_id: Product.query.get(comp.component_id).product_name for comp in child_components}

    # Sort the components by the names stored in the dictionaries, case-insensitive
    sorted_product_components = sorted(product_components, key=lambda x: component_product_names.get(x.product_id, "").lower())
    sorted_child_components = sorted(child_components, key=lambda x: component_product_name.get(x.component_id, "").lower())

    # Check if the user has 'editor' permission
    user_has_editor_permission = permissions.opl_editor_permission.can()


    user_is_admin = permissions.opl_editor_permission.can()

    if product.is_admin_only and not user_is_admin:
        flash('Product not found.', 'error')
        return redirect(url_for('view_routes.view_products'))

    # Fetch the associated product logs
    product_logs = retry_db_operation(lambda: ProductLog.query.filter_by(product_id=product_id).order_by(ProductLog.edit_date.desc()).all())

    return render_template('opl/view.html',
                           product=product,
                           product_types=product_types,
                           sorted_product_components=sorted_product_components,
                           sorted_child_components=sorted_child_components,
                           portfolios=portfolios,
                           partner_choices=partner_choices,
                           component_choices=component_choices,
                           product_notes=product_notes,
                           product_references=product_references,
                           product_aliases=product_aliases,
                           product_mkt_life=product_mkt_life,
                           product_partners=product_partners,
                           product_components=product_components,
                           child_components=child_components,
                           component_product_names=component_product_names,
                           component_product_name=component_product_name,
                           user_is_admin=user_is_admin,
                           user_has_editor_permission=user_has_editor_permission,
                           product_logs=product_logs)



{% extends 'base.html' %}

{% block heading %}
<h2 class="pf-v5-c-title pf-m-xl">{{ product.product_name }}</h2>
{% endblock %}

{% block content %}
{% if product %}
<div id="product-details">

    <!-- Date information -->
    <div class="pf-v5-l-flex pf-m-row pf-m-align-items-center pf-m-justify-content-flex-end">
        <div class="pf-v5-c-card">
            <div class="pf-v5-c-card__body">
                <b>Product created on:</b> {{ product.created.strftime('%B %d, %Y') }}<br>
                <b>Product last updated on:</b> {{ product.last_updated.strftime('%B %d, %Y') }}
            </div>
        </div>
    </div>
    
    <!-- Product Information -->

    {% if product.product_name or product_types or product.product_description or portfolios or
    product.product_notes.first() %}
    <fieldset class="pf-v5-c-form pf-m-horizontal">
        <legend class="pf-v5-c-title">Product information</legend>

        {% if product.product_name %}
        <div class="pf-v5-c-form__field">
            <label class="pf-v5-c-form__label">
                <span class="pf-v5-c-form__label-text">Product name</span>
            </label>
            <div class="pf-v5-c-form__field-control">
                {{ product.product_name }}
            </div>
        </div>
        {% endif %}

        {% if product_types %}
        <div class="pf-v5-c-form__field">
            <label class="pf-v5-c-form__label"">
                <span class="pf-v5-c-form__label-text">Product type</span>
            </label>
            <div class="pf-v5-c-form__field-control">
                <ul id="product_types" class="pf-v5-c-list">
                    {% for product_type in product_types %}
                    <li>{{ product_type.product_type }}</li>
                    {% endfor %}
                </ul>
        
            </div>
        </div>
        {% endif %}

        {% if product.product_description %}
        <div class="pf-v5-c-form__field">
            <label class="pf-v5-c-form__label">
                            <span class=" pf-v5-c-form__label-text">Product description</span>
            </label>
            <div id="product-description-view" class="pf-v5-c-form__field-control">
                {{ product.product_description | safe }}
            </div>
        </div>
        {% endif %}

        {% if portfolios %}
        <div class="pf-v5-c-form__field">
            <label class="pf-v5-c-form__label">
                <span class="pf-v5-c-form__label-text">Portfolio</span>
            </label>
            <div class="pf-v5-c-form__field-control">
                <div class="pf-v5-c-form__control">
                    <ul id="portfolios" class="pf-v5-c-list">
                        {% for portfolio in portfolios %}
                        <li>{{ portfolio.category_name }}</li>
                        {% endfor %}
                    </ul>
                </div>
            </div>
        </div>
        {% endif %}

        {% set first_note = product.product_notes | first %}
        {% if first_note and first_note.product_note %}
        
            <div class="pf-v5-c-form__field">
                <label class="pf-v5-c-form__label">
                    <span class="pf-v5-c-form__label-text">Product notes</span>
                </label>
                <div class="pf-v5-c-form__field-control">
                    {{ first_note.product_note }}
                </div>
            </div>
        {% endif %}
    </fieldset>
    {% endif %}

    <!-- Product Parent/Components Information -->

    {% if sorted_product_components or sorted_child_components %}
    <fieldset class="pf-v5-c-form pf-m-horizontal">
        <legend class="pf-v5-c-title">Product taxonomy</legend>
        <div class="pf-v5-l-grid pf-m-gutter relationship-info">
            <!-- Product Parent Information -->
            {% if sorted_product_components %}
            <div class="pf-v5-l-grid__item pf-m-6-col parent-info">
                {% for component in sorted_product_components %}
                {% set component_name = component_product_names[component.product_id] %}
                {% if component_name %}
                <p>
                    {{ component.component_type | capitalize }} of
                    <a href="{{ url_for('view_routes.view_product_details', product_id=component.product_id) }}">
                        {{ component_name }}
                    </a>
                </p>
                {% endif %}
                {% endfor %}
            </div>
            {% endif %}
    
            <!-- Child Components -->
            {% if sorted_child_components %}
            <div class="pf-v5-l-grid__item pf-m-6-col child-info">
                <span><b>Contains</b></span>
                {% for component in sorted_child_components %}
                {% set child_name = component_product_name[component.component_id] %}
                {% if child_name %}
                <p>
                    <a href="{{ url_for('view_routes.view_product_details', product_id=component.component_id) }}">
                        {{ child_name }}
                    </a> ({{ component.component_type }})
                </p>
                {% endif %}
                {% endfor %}
            </div>
            {% endif %}
        </div>
    </fieldset>
    {% endif %}

    <!-- Product Reference Information -->

    {% if product_references %}
    <fieldset class="pf-v5-c-form pf-m-horizontal">
        <legend class="pf-v5-c-title">Product reference information</legend>
        <div id="product-references" class="pf-v5-l-grid pf-m-gutter">
            <div class="pf-v5-l-grid__item pf-m-6-col">
                <label class="pf-v5-c-form__label">
                    <span class="pf-v5-c-form__label-text">Product reference</span>
                </label>
            </div>
            <div class="pf-v5-l-grid__item pf-m-6-col">
                <label class="pf-v5-c-form__label">
                    <span class="pf-v5-c-form__label-text">Reference description</span>
                </label>
            </div>
        
            {% for reference in product_references %}
            <div class="pf-v5-l-grid__item pf-m-6-col">
                {% if reference.product_link %}
                <div class="pf-v5-c-form__field">
                    <span class="pf-v5-c-form__control product-reference-wrap">
                        <a href="{{ reference.product_link }}" target="_blank">{{ reference.product_link }}</a>
                    </span>
                </div>
                {% endif %}
            </div>
            <div class="pf-v5-l-grid__item pf-m-6-col">
                {% if reference.link_description %}
                <div class="pf-v5-c-form__field">
                    <span class="pf-v5-c-form__control product-reference-wrap">{{ reference.link_description }}</span>
                </div>
                {% endif %}
            </div>
            {% endfor %}
        </div>
        </fieldset>
    {% endif %}

    <!-- Product Status Details -->

    {% if product.deprecated or product.upcoming_change or product.product_status or product.product_status_detail %}
    <fieldset class="pf-v5-c-form pf-m-horizontal">
        <legend class="pf-v5-c-title">Product status information</legend>
    
        {% if product.deprecated %}
        <div class="pf-v5-c-form__field">
            <label class="pf-v5-c-form__label">
                <span class="pf-v5-c-form__label-text">Deprecated</span>
            </label>
            <div class="pf-v5-c-form__field-control">
                {{ "Yes" if product.deprecated else "No" }}
            </div>
        </div>
        {% endif %}
    
        {% if product.upcoming_change %}
        <div class="pf-v5-c-form__field">
            <label class="pf-v5-c-form__label">
                <span class="pf-v5-c-form__label-text">Upcoming change</span>
            </label>
            <div class="pf-v5-c-form__field-control">
                {{ "Yes" if product.upcoming_change else "No"
                    }}
            </div>
        </div>
        {% endif %}
    
        {% if product.product_status %}
        <div class="pf-v5-c-form__field">
            <label class="pf-v5-c-form__label">
                <span class="pf-v5-c-form__label-text">Status</span>
            </label>
            <div class="pf-v5-c-form__field-control">
                {{ product.product_status }}
            </div>
        </div>
        {% endif %}
    
        {% if product.product_status_detail %}
        <div class="pf-v5-c-form__field">
            <label class="pf-v5-c-form__label">
                <span class="pf-v5-c-form__label-text">Status details</span>
            </label>
            <div class="pf-v5-c-form__field-control">
                {{ product.product_status_detail }}
            </div>
        </div>
        {% endif %}
    </fieldset>
    {% endif %}

    <!-- Product Alias Information -->

    {% if product_aliases %}
    <fieldset class="pf-v5-c-form pf-m-horizontal">
        <legend class="pf-v5-c-title">Product alias information</legend>
        <p><b>Note:</b> Always use full product name on first use and whenever clarity is needed. After first use, you may
            use approved short
            forms or acronyms. Tech docs (technical, customer-facing documentation) refers to non-marketing, non-sales
            content used
            to train customers, assist with installation, etc., such as getting started guides, Jira/Bugzilla entries, and
            support
            case summaries.</p>
        <div class="pf-v5-c-table pf-m-grid-md">
            <!-- Table Headers -->
            <div class="pf-v5-c-table__header">
                <div class="pf-v5-c-table__column"><strong>Alias name</strong></div>
                <div class="pf-v5-c-table__column"><strong>Approved for general use</strong></div>
                <div class="pf-v5-c-table__column"><strong>Previous name</strong></div>
                <div class="pf-v5-c-table__column"><strong>Approved for tech docs</strong></div>
                <div class="pf-v5-c-table__column"><strong>Approved for tech docs code/CLI</strong></div>
                <div class="pf-v5-c-table__column"><strong>Alias notes</strong></div>
            </div>
            <!-- Each Row Represents a Set of Alias Information -->
            {% for alias in product_aliases %}
            <div class="pf-v5-c-table__row">
                <div class="pf-v5-c-table__column">{{ alias.alias_name }}</div>
                <div class="pf-v5-c-table__column">
                    {% if alias.alias_approved %}
                    <strong>Yes</strong>
                    {% else %}
                    No
                    {% endif %}
                </div>
                <div class="pf-v5-c-table__column">
                    {% if alias.previous_name %}
                    <strong>Yes</strong>
                    {% else %}
                    No
                    {% endif %}
                </div>
                <div class="pf-v5-c-table__column">
                    {% if alias.tech_docs %}
                    <strong>Yes</strong>
                    {% else %}
                    No
                    {% endif %}
                </div>
                <div class="pf-v5-c-table__column">
                    {% if alias.tech_docs_cli %}
                    <strong>Yes</strong>
                    {% else %}
                    No
                    {% endif %}
                </div>
                <div class="pf-v5-c-table__column">{{ alias.alias_notes or "N/A" }}</div>
            </div>
            {% endfor %}
        </div>
    </fieldset>
    {% endif %}

    <!-- Product Release Information -->

    <div class="pf-v5-l-grid pf-m-gutter">
        {% if product_mkt_life.product_release or product_mkt_life.product_release_detail or
        product_mkt_life.product_release_link %}
        <fieldset class="pf-v5-c-form pf-m-horizontal pf-v5-l-grid__item pf-m-6-col">
            <legend class="pf-v5-c-title">Product release information</legend>
    
            {% if product_mkt_life.product_release %}
            <div class="pf-v5-c-form__field">
                <label class="pf-v5-c-form__label">
                    <span class="pf-v5-c-form__label-text">Release date</span>
                </label>
                <div class="pf-v5-c-form__field-control">
                {{ product_mkt_life.product_release.strftime('%d %B %Y') }}
                </div>
            </div>
            {% endif %}
    
            {% if product_mkt_life.product_release_detail %}
            <div class="pf-v5-c-form__field">
                <label class="pf-v5-c-form__label">
                    <span class="pf-v5-c-form__label-text">Release detail</span>
                </label>
                <div class="pf-v5-c-form__field-control">
                    {{ product_mkt_life.product_release_detail }}
                </div>
            </div>
            {% endif %}
    
            {% if product_mkt_life.product_release_link %}
            <div class="pf-v5-c-form__field">
                <label class="pf-v5-c-form__label">
                    <span class="pf-v5-c-form__label-text">Release reference</span>
                </label>
                <div class="pf-v5-c-form__field-control">
                    <a href="{{ product_mkt_life.product_release_link }}" target="_blank">{{
                    product_mkt_life.product_release_link }}</a>
                </div>
            </div>
            {% endif %}
        </fieldset>
        {% endif %}
    
        <!-- Product EOL Information -->
        {% if product_mkt_life.product_eol or product_mkt_life.product_eol_detail or product_mkt_life.product_eol_link %}
        <fieldset class="pf-v5-c-form pf-m-horizontal pf-v5-l-grid__item pf-m-6-col">
            <legend class="pf-v5-c-title">Product end of life information</legend>
    
            {% if product_mkt_life.product_eol %}
            <div class="pf-v5-c-form__field">
                <label class="pf-v5-c-form__label">
                    <span class="pf-v5-c-form__label-text">Product end of life (EOL) date</span>
                </label>
                <div class="pf-v5-c-form__field-control">
                {{ product_mkt_life.product_eol.strftime('%d %B %Y') }}
                </div>
            </div>
            {% endif %}
    
            {% if product_mkt_life.product_eol_detail %}
            <div class="pf-v5-c-form__field">
                <label class="pf-v5-c-form__label">
                    <span class="pf-v5-c-form__label-text">Product end of life (EOL) details</span>
                </label>
                <div class="pf-v5-c-form__field-control">
                {{ product_mkt_life.product_eol_detail }}
                </div>
            </div>
            {% endif %}
    
            {% if product_mkt_life.product_eol_link %}
            <div class="pf-v5-c-form__field">
                <label class="pf-v5-c-form__label">
                    <span class="pf-v5-c-form__label-text">Product end of life (EOL) reference</span>
                </label>
                <div class="pf-v5-c-form__field-control">
                <a href="{{ product_mkt_life.product_eol_link }}" target="_blank">{{ product_mkt_life.product_eol_link
                    }}</a>
                    </div>
            </div>
            {% endif %}
        </fieldset>
    </div>
    {% endif %}

    <!-- Product Partners Information -->

    {% if product_partners %}
    <fieldset class="pf-v5-c-form pf-m-horizontal">
        <legend class="pf-v5-c-title">Product partners information</legend>
        <div class="pf-v5-c-form__field">
            <div class="pf-v5-c-form__group-control">
                <label class="pf-v5-c-form__label">
                    <span class="pf-v5-c-form__label-text">In Partnership with</span>
                </label>
                <div class="pf-v5-c-form__field-control">
                    <ul id="product_partners" class="pf-v5-c-list">
                        {% for partner in product_partners | sort(attribute='partner.partner_name') %}
                        <li>{{ partner.partner.partner_name }}</li>
                        {% endfor %}
                    </ul>
                </div>
            </div>
        </div>
    </fieldset>
    {% endif %}

    <!-- Product Notes Information -->

    {% if product_logs %}
    <fieldset class="pf-v5-c-form pf-m-horizontal">
        <legend class="pf-v5-c-title">Notes and changelog</legend>
        <div id="product-notes" class="pf-v5-c-table pf-m-grid-md">
            <div class="pf-v5-c-table__header">
                <div class="pf-v5-c-table__column"><strong>Date</strong></div>
                <div class="pf-v5-c-table__column"><strong>Notes</strong></div>
                <div class="pf-v5-c-table__column"><strong>Added By</strong></div>
            </div>
            <div class="pf-v5-c-table__body">
                {% for product_log in product_logs %}
                <div class="pf-v5-c-table__row">
                    <div class="pf-v5-c-table__column">{{ product_log.edit_date.strftime('%d %B %Y') }}</div>
                    <div class="pf-v5-c-table__column">{{ product_log.edit_notes }}</div>
                    <div class="pf-v5-c-table__column">{{ product_log.username }}</div>
                </div>
                {% endfor %}
            </div>
        </div>
    </fieldset>
    {% endif %}
    
</div>
{% else %}
<p>No product details available.</p>
{% endif %}
<a href="{{ url_for('view_routes.view_products') }}" class="pf-v5-c-button pf-m-primary">View more products</a>
<a href="{{ url_for('edit_routes.edit_product_details', product_id=product.product_id) }}"
    class="pf-v5-c-button pf-m-primary">Edit this product</a>

{% if user_has_editor_permission %}
<a href="{{ url_for('delete_routes.confirm_delete_product', product_id=product.product_id) }}"
        class="pf-v5-c-button pf-m-danger">Delete Product</a>
{% endif %}

{% endblock %}
                           


