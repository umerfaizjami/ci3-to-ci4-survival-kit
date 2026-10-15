# 📖 The Master CI3 to CI4 Cheat Sheet

This document provides side-by-side comparisons of the most common CodeIgniter 3 patterns and their CodeIgniter 4 equivalents. 

> 💡 **Pro Tip:** Use your browser's search (Ctrl+F / Cmd+F) to quickly find the CI3 code you are trying to replace.

---

## 1. Routing

### CodeIgniter 3
```php
// application/config/routes.php
$route['default_controller'] = 'welcome';
$route['products/(:any)'] = 'catalog/product_lookup/$1';
$route['news/(:num)'] = 'news/article/$1';
```

### CodeIgniter 4
```
// app/Config/Routes.php
$routes->get('products/(:any)', 'Catalog::productLookup/$1');
$routes->get('news/(:num)', 'News::article/$1');
// Note: CI4 handles the default controller via $routes->setDefaultController('Home');
```
> 💡 **Why it changed**: CI4 uses an object-oriented routing system ($routes) instead of a simple array. This allows for better route grouping, HTTP method specificity (get, post, put), and easier filtering.

# 2. Database Query Builder
### CodeIgniter 3
```php
// Loading and querying
$this->db->where('status', 'active');
$this->db->order_by('created_at', 'DESC');
$query = $this->db->get('users');
$result = $query->result(); // Returns array of objects
$row = $query->row();       // Returns single object
```


### CodeIgniter 4

```php
// Using the Query Builder directly
$builder = $db->table('users');
$builder->where('status', 'active');
$builder->orderBy('created_at', 'DESC');
$result = $builder->get()->getResult(); // Returns array of objects
$row = $builder->get()->getRow();       // Returns single object

// OR using the Model (Recommended in CI4)
$userModel = new \App\Models\UserModel();
$result = $userModel->where('status', 'active')->findAll();
$row = $userModel->find($id);
```

> 💡 **Why it changed**:  CI4 separates the database connection from the query builder instance. This improves testability, prevents global state pollution, and aligns with modern PHP standards. Using Models is now highly encouraged.

# 3. Loading Models & Libraries

### CodeIgniter 3


```php
// Loading a model
$this->load->model('User_model');
$this->User_model->get_users();

// Loading a library
$this->load->library('email');
$this->email->from('test@example.com');
```

### CodeIgniter 4

```php

// Instantiating a model (PSR-4 Autoloading)
$userModel = new \App\Models\UserModel();
$userModel->getUsers();

// Loading a service (Library equivalent)
$email = \Config\Services::email();
$email->setFrom('test@example.com');

```

> 💡 **Why it changed**: CI4 relies on PHP namespaces and PSR-4 autoloading. The "magic" $this->load methods are replaced by explicit instantiation or the Service container. This makes your code predictable, easier to debug, and fully compatible with modern IDE auto-completion.

# 4. Form Validation

### CodeIgniter 3


```php
$this->load->library('form_validation');
$this->form_validation->set_rules('username', 'Username', 'required|min_length[5]');

if ($this->form_validation->run() == FALSE) {
    $this->load->view('myform');
} else {
    $this->load->view('formsuccess');
}
```

### CodeIgniter 4

```php

// Inside a Controller
$rules = [
    'username' => 'required|min_length[5]'
];

if (!$this->validate($rules)) {
    return view('myform', ['validation' => $this->validator]);
} else {
    return view('formsuccess');
}

```

> 💡 **Why it changed**: CI4 provides a cleaner, more intuitive API. The global session() helper function removes the need to manually load the library, and the methods (set, get) are more consistent with modern PHP frameworks.
