# lumen-form-requests

<p align="center">
<a href="LICENSE"><img src="https://img.shields.io/badge/license-MIT-brightgreen.svg?style=flat-square" alt="Software License"></img></a>
<a href="https://github.com/iocaste/lumen-form-requests/releases"><img src="https://img.shields.io/github/release/iocaste/lumen-form-requests.svg?style=flat-square" alt="Latest Version"></img></a>
<a href="https://packagist.org/packages/iocaste/lumen-form-requests"><img src="https://img.shields.io/packagist/dt/iocaste/lumen-form-requests.svg?style=flat-square" alt="Total Downloads"></img></a>
</p>

Missing form requests functionality for lumen, ported from laravel framework.

# Installation

* Install as composer package

```bash
composer require noitran/lumen-form-requests
```

* Open your bootstrap/app.php and register as service provider  

```php
$app->register(Noitran\Form\Providers\FormRequestServiceProvider::class);
```

# Usage

Refer to the official laravel documentation about form request usage

<a href="https://laravel.com/docs/5.7/validation#form-request-validation">https://laravel.com/docs/5.7/validation#form-request-validation</a>


### Example Request

```php
<?php

namespace App\Http\Requests;

use Noitran\Microservice\Foundation\Http\Requests\Request;

class CreateUserRequest extends Request
{
    /**
     * Determine if the user is authorized to make this request.
     *
     * @return bool
     */
    public function authorize(): bool
    {
        return true;
    }

    /**
     * Get the validation rules that apply to the request.
     *
     * @return array
     */
    public function rules(): array
    {
        $rules = [
            'email' => [
                'required',
                'email',
                'unique:users,email',
            ],
            'password' => [
                'required',
            ],
        ];
    }
}
```

### Usage in Controller

```php
<?php

namespace App\Http\Controllers;

use App\Http\Requests\CreateUserRequest;
use App\Http\Controllers\Controller;

class UsersController extends Controller
{
    /**
     * Store a new user.
     *
     * @param CreateUserRequest $request
     * @return Response
     */
    public function store(CreateUserRequest $request)
    {
        // store user
    }
}
```
