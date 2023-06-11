---
title: Laravel-file-storing
date: 05/06/2023
tags: laravel php file-upload
---

# **Laravel-file-storing** 202306051800 
> **eb4ec5**



## Laravel File Storage

### Storing a file using request
Start by creating a Request through php artisan:

```bash
php artisan make:request UpdateAvatarRequest
```

This will create the UpdateAvatarRequest class in the app/Http/Requests folder.

Set the rule for the request:

```php
<?php

namespace App\Http\Requests;

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

After that inside our AvatarControler we need to store the file in the database:
```php
use App\Http\Controllers\AvatarController;
use App\Http\Requests\UpdateAvatarRequest;
use Illuminate\Http\Request;
use Illuminate\Support\Facades\Storage;
use Intervention\Image\Facades\Image;

class AvatarController extends Controller
{
    public function update(UpdateAvatarRequest $request)
    {
        $avatar = $request->avatar;
        $filename = time() . '.' . $avatar->extension();
        $avatar->storeAs('avatars', $filename);
        $user = auth()->user();
        $user->avatar = $filename;
        $user->save();
        return back();    
        }
}
```

### Making the file public and giving it a relative path

To make the file public and available to load, we need to first create a symbolic link to the file:
```bash
php artisan storage:link
```

After that in our Controller we need to provide the relative path of the file before storing the path on the database.
Like we did above or:
```php
public function update(UpdateAvatarRequest $request)
    {
        // Find the user that is currently authenticated and update their avatar with the new one sent in the request
        $user = User::find(auth()->user()->id);

        // store the file in the public folder
        $file = $request->file('avatar')->store('avatars', 'public');
        // dd($file);
        $user->update(['avatar' => 'storage/' . $file ]);

        // Redirect back to the page that made the request with a message indicating that the avatar was successfully changed
        return back()->with('message', 'Avatar Successfully changed!');
    }
```
