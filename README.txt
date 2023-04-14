Do at least ONE of the following tasks: refactor is mandatory. Write tests is optional, will be good bonus to see it. 
Please do not invest more than 2-4 hours on this.
Upload your results to a Github repo, for easier sharing and reviewing.

Thank you and good luck!



Code to refactor
=================
1) app/Http/Controllers/BookingController.php
2) app/Repository/BookingRepository.php

Code to write tests (optional)
=====================
3) App/Helpers/TeHelper.php method willExpireAt
4) App/Repository/UserRepository.php, method createOrUpdate


----------------------------

What I expect in your repo:

X. A readme with:   Your thoughts about the code. What makes it amazing code. Or what makes it ok code. Or what makes it terrible code. How would you have done it. Thoughts on formatting, structure, logic.. The more details that you can provide about the code (what's terrible about it or/and what is good about it) the easier for us to assess your coding style, mentality etc

And 

Babar's Thoughts
----------------
    reference to Booking Controllers
    Ans: The code is not elegant as it should be, developer used OOP approach in it that is good engough with respect to code execution.
    But code excution speed is matters and that will be efficient if we use MVC standard, OOP is good when You are in single class with single object, 
    according to my opnion code will be more elegant if we try MVC standard approach e.g

    function reference: Booking->index
    
    we can use ternary expression single line code that will result more fast as compare to current approach.
    we should use as 

    current
    -----------
    if($user_id = $request->get('user_id')) {

            $response = $this->repository->getUsersJobs($user_id);

        }
    more elegant will be
    --------------------
   $response =  $request->get('user_id') ?  $response = $this->repository->getUsersJobs($user_id) : other statement option
----------------------------------
   function reference : Booking->show
   
   it can be in single line of code as
   
   old
   ----
    $job = $this->repository->with('translatorJobRel.user')->find($id);

        return response($job);

    my suggestions
    --------------
 return response($this->repository->with('translatorJobRel.user')->find($id));

 as vice versa with other function code of Booking Controller.
 Let talk about the BookingRepository

 function getUsersJobs() need to use relationship as data is pulling from different tables with reference to ids, so ids base on relationship
 code can be more efficient if we will use single base query with relation. but here compiler need to run queries not query that cause bad effect on
 1. Complier efficincy
 2. Processor Cache (user of more enough variables).
 in Booking Repository array value can be check with in_array with ternary expression and other such type of function to avoid 
 the if-else large structure.
 function changeStatus() developer use switch statement that is very nice approach to avoid if-else structure as code is looking very beautiful.
 useless code should be remove not comment, that usually casue interption in understading of code flow.
 function store() line 207 developer user in_array that is good but it will more elegant if he goes with switch statement also.

----------------

TeHelper

  public static function fetchLanguageFromJobId($id)
    {
        $language = Language::findOrFail($id);
        return $language1 = $language->language;
    }

is wrong code
it should be as
 public static function fetchLanguageFromJobId($id)
    {
        $language = Language::findOrFail($id);
        return $language

        or it may be as 
        return Language::findOrFail($id);
    }


wrong function
 public static function getUsermeta($user_id, $key = false)
    {
        return $user = UserMeta::where('user_id', $user_id)->first()->$key;
        if (!$key)
            return $user->usermeta()->get()->all();
        else {
            $meta = $user->usermeta()->where('key', '=', $key)->get()->first();
            if ($meta)
                return $meta->value;
            else return '';
        }
    }
Corrent function
 public static function getUsermeta($user_id, $key = false)
    {
        $user = '';
        if (!$key)
            $user =  $user->usermeta()->get()->all();
        else {
            $meta = $user->usermeta()->where('key', '=', $key)->get()->first();
            if ($meta)
                $user =  $meta->value;
            
        }
        return $user;
    }

wrong approach
$jobs = array();
        foreach ($jobs_ids as $job_obj) {
            $jobs[] = Job::findOrFail($job_obj->id);
        }
        return $jobs;

Corrent approach
    use intital $jobs variable inside loop as it is already declare as array
    
Y.  Refactor it if you feel it needs refactoring. The more love you put into it. The easier for us to asses your thoughts, code principles etc


IMPORTANT: Make two commits. First commit with original code. Second with your refactor so we can easily trace changes. 


NB: you do not need to set up the code on local and make the web app run. It will not run as its not a complete web app. This is purely to assess you thoughts about code, formatting, logic etc


===== So expected output is a GitHub link with either =====

1. Readme described above (point X above) + refactored code 
OR
2. Readme described above (point X above) + refactored core + a unit test of the code that we have sent

Thank you!


