---
title: laravel-validation
date: 05/06/2023
tags: laravel php validation
---

# **laravel-validation** 202306050346 
> **97fa6c**

  

## Laravel validation

### validating a request
```php
// Validate the request
        $validated = $request->validate([
            'avatar' => 'required|image|mimes:jpeg,png,jpg,gif,svg|max:2048',
        ]);

        // If not validated, return back with an error message
        if (!$validated) {
            return back()->withErrors($validated)->withInput();
        }
```

This snippet works as intended; however, there is a better way of doing it.
Outside of the controller.

### Form request validation
Start by creating our service request
`php artisan make:request UpdateAvatarRequest`

By making a form request validation file for our controller.
All the logic of validation is relegated to the Form request handler.

The form request handler:
```php
use Illuminate\Foundation\Http\FormRequest;

class UpdateAvatarRequest extends FormRequest
{
    /**
     * Determine if the user is authorized to make this request.
     */
    public function authorize(): bool
    {
        return true;
    }

    /**
     * Get the validation rules that apply to the request.
     *
     * @return array<string, \Illuminate\Contracts\Validation\ValidationRule|array|string>
     */
    public function rules(): array
    {
        return [
            'avatar' => 'required|image|mimes:jpeg,png,jpg,gif,svg|max:2048',
        ];
    }
}
```
