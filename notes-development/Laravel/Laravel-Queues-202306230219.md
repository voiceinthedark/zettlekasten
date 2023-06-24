---
title: Laravel-Queues
date: 23/06/2023
tags: Laravel Queues asynchronous-tasks
---

# **Laravel-Queues** 202306230219 
> **4ed552**

  

## Queuing Jobs
To Add a job to a queue we need to create a queue job first: `php atrisan make:job <job-name>`

Once created we can put the task to be queued in the `handle()` method of our job class.
After that we can run the queue by calling the `dispatch()` method on our Job Class.

Before we can dispatch the job we need to create a table to hold the jobs.
If we decided to use the database instead of redis we need to configure the `.env` file as such.

Once done we need to create the queue table in the database.
`php artisan queue:table`
`php artisan migrate`

Now that our table is created, Jobs can be queued. But in order for the jobs to be processed we need to
call the artisan command work: `php artisan queue:work`

## Handling failure
To handle a job failure we need to implement the `failed()` method inside the job class.
This method will execute if the queued job failed to be processed.


