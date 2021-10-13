# Laravel-8-Rest-API-Simple-Example
Simple Example laravel rest API for Beginner

# Conroller Code 

```
<?php

namespace App\Http\Controllers;

use App\Models\User;
use App\Http\Controllers\Controller;
use Illuminate\Http\Request;

class  UserController extends Controller{

    //create new user
    public function createUser(Request $request){
        $user = User::create($request->all());
        return response()->json($user);
    }
    
    //update user details
    
    public function updateUser(Request $request, $id){
        $user = User::find($id);
        $user->first_name = $request->input('first_name');
        $user->last_name =  $request->input('last_name');
        $user->email_address = $request->input('email_address');
        $user->save();
        return response()->json($user);
    }


    //view user
    public function viewUser($id){
     $user =  User::find($id);
            return response()->json($user);
    }


    //delete user(
    public function deleteUser($id){
        $user =  User::find($id);
        $user->delete();

        return response()->json('Removed successfully');
    }

    //list users
    public function index(){
        $user =User::all();
        return response()->json($user);
    }

} 
?>

```

# Model Code 

```
<?php

namespace App\Models;

use Illuminate\Auth\Authenticatable;
use Illuminate\Contracts\Auth\Access\Authorizable as AuthorizableContract;
use Illuminate\Contracts\Auth\Authenticatable as AuthenticatableContract;
use Illuminate\Database\Eloquent\Factories\HasFactory;
use Illuminate\Database\Eloquent\Model;
use Laravel\Lumen\Auth\Authorizable;

class User extends Model implements AuthenticatableContract, AuthorizableContract
{
    use Authenticatable, Authorizable, HasFactory;

    /**
     * The attributes that are mass assignable.
     *
     * @var array
     */
    protected $fillable =['first_name', 'last_name', 'email_address',];

    /**
     * The attributes excluded from the model's JSON form.
     *
     * @var array
     */
    protected $hidden = [
        'password',
    ];
}
view raw

```



# User table migration
```
<?php

use Illuminate\Database\Migrations\Migration;
use Illuminate\Database\Schema\Blueprint;
use Illuminate\Support\Facades\Schema;

class CreateUsersTable extends Migration
{
    /**
     * Run the migrations.
     *
     * @return void
     */
    public function up()
    {
        Schema::create('users', function (Blueprint $table) {
            $table->increments('id');
            $table->string('first_name');
            $table->string('last_name');
            $table->string('email_address');
            $table->timestamps();
        });
    }

    /**
     * Reverse the migrations.
     *
     * @return void
     */
    public function down()
    {
        Schema::dropIfExists('users');
    }
}

```

!code By Arun Android


