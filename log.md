# 100 Days Of Code - Log

### Day 7: January 27, 2019

**Today's Progress**: Got a working version of the recipe model, implemented the controller/view, and updated the EFCore database to recognize the new recipe model.   

**Thoughts:** I'm still not sure what's going on in the Identity library from Day 6, but I decided to move on for now and will continue researching at a later time.  I'm feeling good about the Recipe model I created, and my next steps are more front-end in nature.  I took care of the back-end work today with setting up the model and controller, but I need to modify the view to suit my needs.

**Link to work:** <br>
[MealPlanner](https://github.com/delsuckahh/meal-planner/tree/master/MealPlanner)<br>

### Day 6: January 26, 2019

**Today's Progress**: Continued thinking/planning data models in regards to recipies, meals, and ingredients.  Researched and read documentation regarding the Identity library for ASP.NET provided by the Entity Framework  

**Thoughts:** I'm leaving today feeling confused.  I'm trying to understand how the Identity library works in regards to authorization.  For example, if you sign in to the app and click your username at the top right, it takes you to a user page.  I CANNOT find where this is coded.  I see the \_LoginPartial.cshtml file in View/Shared.  That reveals to me that clicking on the username invokes a controller in area "Identity".  HOWEVER, I can't find this controller.  Check this out:
```
<li>
    <a asp-area="Identity" asp-page="/Account/Manage/Index" title="Manage">Hello @UserManager.GetUserName(User)!</a>
</li>
```     
So, I do see an Areas folder, and I can see this path: Areas/Identity/Pages/\_ViewStart.cshtml.  \_ViewStart just points to the shared \_Layout view.  But I do NOT see any controller, so how does it interpret "Account/Manage/Index"?  It's my understanding that there should be an AccountController somewhere, which has either/both a manage or/and index method.  I'm having a hard time finding the documentation on this...

**Link to work:** <br>
[MealPlanner](https://github.com/delsuckahh/meal-planner/tree/master/MealPlanner)<br>


### Day 5: January 25, 2019

**Today's Progress**: Started on the meal planning app; added authorization and started planning out the classes/models.  

**Thoughts:** I'm a little overwhelmed on how to design the models for future proofing / reusability.  I want to make sure that what I code can be added on to and maintained and edited easily in the future.  I want to make sure that what I design makes sense and will work for what I'm trying to accomplish.  Does "food" need to be it's own class?  Or should it just be a property of the "recipe" class?  Does "meal" need it's own class, or can that just be the title of the recipe class?  I had fun playing around with authorization of the app and linking views to controllers.  I may need to step back and think about the design of the data before I go any further.

**Link to work:** <br>
[MealPlanner](https://github.com/delsuckahh/meal-planner/tree/master/MealPlanner)<br>

### Day 4: January 24, 2019

**Today's Progress**: Finished up Microsoft's MVC tutorial. 

**Thoughts:** Another reading/tutorial heavy day.  I can already see the benefit in going through the tutorials; I was even able to use what I've learned so far at work today.  An application that we support uses .NET and Oracle, and I was able to follow along and help a co-worker (shoutout to my boi Sposi) debug an issue today.  I was able to identify and understand lambda functions, async/await calls, and the interactions between models, views, and controllers.  I didn't spend quite an hour this evening in tutorials.  I finished a bit early, but since my next step is to actually start on my project, I'm going to wait until tomorrow so I can dedicate more uninterrupted time towards it.  Tomorrow I hope to progress in creating a login for my webapp using the SQL Server functionality built in the ASP.NET framework.  

**Link to work:** <br>
[MvcMovie](https://github.com/delsuckahh/MvcMovie/tree/master/MvcMovie)<br>
[Microsoft Tutorial](https://docs.microsoft.com/en-us/aspnet/core/tutorials/first-mvc-app/adding-view?view=aspnetcore-2.1&tabs=visual-studio)<br>

### Day 3: January 23, 2019

**Today's Progress**: Continued with Microsoft's MVC tutorial, finished one more section. 

**Thoughts:** I did a LOT of reading today.  I spent some time throughout the day finishing up the tutorial at TutorialsPoint, which gave a good overview of the interacting pieces of ASP.NET.  I went off a bit of a tangent from the Microsoft Tutorial and read up on Async/Await.  The documentation I've been reading hasn't covered that in detail even though it's present in the code.  I feel pretty comfortable with that terminology now, and I'm on track to finish the tutorial by the end of the week.  I've got high hopes and ambitions for my web app idea of a meal planner, so I'll be excited to get started on that here soon.

**Link to work:** <br>
[MvcMovie](https://github.com/delsuckahh/MvcMovie/tree/master/MvcMovie)<br>
[Microsoft Tutorial](https://docs.microsoft.com/en-us/aspnet/core/tutorials/first-mvc-app/adding-view?view=aspnetcore-2.1&tabs=visual-studio)<br>
[TutorialsPoint](https://www.tutorialspoint.com/asp.net/)<br>

### Day 2: January 22, 2019

**Today's Progress**: Followed along Microsoft's MVC tutorial and finished up two sections.

**Thoughts:** Today was a good day.  I determined what my "problem" was yesterday; I can read and understand c# just fine, I just don't quite understand the MVC model yet.  I made really good progress in understanding the relationship between Models, Views, and Controllers today.  I spent some time throughout the day passively reading documentation about MVC.  Then tonight, during my allotted coding time, I spent time in the interactive tutorial my Microsoft.  I'm still not sure about the async/await keywords and what EXACTLY they do.  I did think this was really cool, though:
```
@{
    ViewData["Title"] = "Welcome";
}

<h2>Welcome</h2>

<ul>
    @for (int i = 0; i < (int)ViewData["NumTimes"]; i++)
    {
        <li>@ViewData["Message"]</li>
    }
</ul>
```
Combining HTML and some actual programming is pretty saucy.

**Link to work:** <br> 
[MvcMovie](https://github.com/delsuckahh/MvcMovie)<br>
[Microsoft Tutorial](https://docs.microsoft.com/en-us/aspnet/core/tutorials/first-mvc-app/adding-view?view=aspnetcore-2.1&tabs=visual-studio)<br>

### Day 1: January 21, 2019

**Today's Progress**: Environment setup (VS 2017). Initial commit of web app. Progressed in MVC tutorial and initial commit.

**Thoughts:** Day number one.  I have high hopes for this challenge.  I am excited and a little nervous.  I overestimated what I actually knew about ASP.NET.  I can recall the terminology, but I'm a bit lost of where to begin.  I've decided to take a couple days to refresh my memory with tutorials.

**Link to work:** <br> 
[MealPlanner](https://github.com/delsuckahh/meal-planner)<br>
[MvcMovie](https://github.com/delsuckahh/MvcMovie)<br>
