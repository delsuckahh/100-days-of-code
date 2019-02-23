# 100 Days Of Code - Log

### Day 27: February 23, 2019

**Today's Progress**: Worked on reading/displaying related records with the Recipe controller and detail view.

**Thoughts:** For those that are actually reading and following my progress, my apologies for missing the past three days.  I'm really trying not to miss a day, let alone 3 days in a row.  Going forward, I'm not going to mention my absences, though.  I've determined that while I AM committed to coding for 100 days, life happens and I probably won't be perfect in coding every single day for an hour.  I've got a family to take care of and stuff comes up.  Anyway, on with the coding update...<br>
<br>
This morning I made some decent progress.  I'm having trouble displaying the related records of Recipe (Ingredient/Instruction).  I did tweak the MealInitializer class to create related records, which will help me in figuring out how to display that data (I can't display what doesn't exist).  Here's what I came up with:<br>
````
protected override void Seed(MealContext context)
        {
            var recipes = new List<Recipe>
            {
                new Recipe{Title="Taco Soup",Description="Its like a taco, but in soup form",PrepTime=30,CookTime=30,Calories=1200,NumServings=4,Course="Dinner",Cuisine="Mexian",},
                new Recipe{Title="Beef Ravioli",Description="Beef stuffed into a noodle, what's not to like?",PrepTime=60,CookTime=50,Calories=2200,NumServings=4,Course="Dinner",Cuisine="Italian",}
            };
            recipes.ForEach(s => context.Recipes.Add(s));
            context.SaveChanges();

            var ingredients = new List<Ingredient>();
            var instructions = new List<Instruction>();
            foreach(Recipe item in recipes)
            {
                ingredients.Add(new Ingredient { RecipeID = item.ID, Item = "Ingredient 1", });
                ingredients.Add(new Ingredient { RecipeID = item.ID, Item = "Ingredient 2", });
                instructions.Add(new Instruction { RecipeID = item.ID, StepNum = 1, Description = "Instruction 1", });
                instructions.Add(new Instruction { RecipeID = item.ID, StepNum = 2, Description = "Instruction 2", });
            }
            ingredients.ForEach(s => context.Ingredients.Add(s));
            instructions.ForEach(s => context.Instructions.Add(s));
            context.SaveChanges();

        }
````
I modifed the the Views/Recipe/Details view to display this new data, but I've not got the controller passing the right content quite yet.  I'm currently getting a <br>
````
Object reference not set to an instance of an object.
````
error, which means I'm not initializing the class right, so it doesn't have access to the data.  I'm looking back through the Conotoso University tutorial for some guidance on that.<br>
**Link to work:** <br>
[MealPlanner](https://github.com/delsuckahh/meal-planner/tree/FreshStart/MealPlanner)<br>
[Tutorial](https://docs.microsoft.com/en-us/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application#learn-how-to-load-related-data)<br>




### Day 26: February 19, 2019

**Today's Progress**: Read a LITTLE documentation.

**Thoughts:** I'll be honest, I was NOT feeling it tonight.  We had family over late for my mother-in-law's birthday.  I looked up some documentation on handling one-to-many relationship in regards to viewing/creating/editing.  Next step for me is to either display and/or create ingredient records for the recipe record.  Not sure how to practically get started with that, but I found a few promising articles on how to handle that.

**Link to work:** <br>
[MealPlanner](https://github.com/delsuckahh/meal-planner/tree/FreshStart/MealPlanner)

### Day 25: February 18, 2019

**Today's Progress**: Worked on the recipe detail view.

**Thoughts:**  Today was good; I solidifed some more of the concepts I learned in the Contoso University tutorial, specifially using a ViewModel class to display related data.  I haven't made any related data records yet (ingredients/instructions), but I made the viewmodel class and was able to successfully display the data passed by the controller.

**Link to work:** <br>
[MealPlanner](https://github.com/delsuckahh/meal-planner/tree/FreshStart/MealPlanner)


### Day 24: February 17, 2019

**Today's Progress**: Started fresh, due to db connection issues.

**Thoughts:**  I started my project over today.  I started the project before I had begun the tutorials, and I felt like I was in a bad place.  I hadn't progressed that much, but my environment was pretty messed up.  I decided to cut my losses and start at the beginning.  The only thing I transferred over was my existing data models.  I copied those over and focused on getting my database connection right.  I felt like I made good progress, although I could not get the seed method to run for some reason.  I was having some issues with building the scaffolded code, which ended up being an issue with my seed method.  I initially left it with default code, but that was causing an object instantiation error.  Commenting out the ContextInitializer string in the web.config file fixed that problem.  I set the seed method to only run on model change.  I made some trivial changes and ran the update-databse commands, but for some reason the seed method was never called.  (Or rather, it never created succesfully - I just realized while typing this out, I could put some logging in that method to see if its being called.  Perhaps it IS called, its just not functioning like I'm intending.)

Edit: I got the seed method to run.  I think for some reason I just wasn't changing enough to cause the DropCreateDatabaseIfModelChanges<MealContext> to trigger.  I changed the database connection name (from MealPlanner1 to MealPlanner2) to force a new database creation when I ran the program.  This caused the seed method to run, and I can see my seeded recipes! Yay!

**Link to work:** <br>
[MealPlanner](https://github.com/delsuckahh/meal-planner/tree/FreshStart/MealPlanner)


### Day 23: February 15, 2019

**Today's Progress**: I broke everything.

**Thoughts:** I screwed up my database connection.  For some reason, I had two database contexts, "ApplicationDbContext" which seems like the default, and "MealPlannerContext" which seems like I somehow made - probably with some scaffolded function.  Where I'm confused, is that the project I worked on in the tutorial had a web.config file, while my project has a appsettings.json file.  One is xml one is json (obviously).  However, I just cannot get the context working like I need to.  Right now my project has a compile error so it does not work at all. RIP.

Note:  I missed yesterday due to technical issues.  I had to resize my harddrive partitions, download some drivers for my GPU, uninstall/reinstall some software, and of course I had to back up my computer before I started all that.  So that took up my entire evening yesterday.  Just so you don't think I'm some sort of slacker or something...

**Link to work:** <br>
[MealPlanner](https://github.com/delsuckahh/meal-planner/tree/ConnectToDB)

### Day 22: February 13, 2019

**Today's Progress**: Got a working version of the data models I'll be using in the meal planning app.

**Thoughts:** It was nice to solidify the concepts I learned in the tutorial, in regards to creating data models.  I have now what I think is my final version of data design.  I'll most likely add some more validations/requirements, but the structure is good.  I have a working index page for the recipes.  Tomorrow, I will modify the controller and view to display the ingredients and instructions - right now, it just shows data from the recipe table itself.

**Link to work:** <br>
[MealPlanner](https://github.com/delsuckahh/meal-planner/tree/IngredientTesting)

### Day 21: February 12, 2019

**Today's Progress**: Completed the 'Contoso University' tutorial by Microsoft.

**Thoughts:** Finally finished up the tutorial tonight.  This last section was neat, it was more just briefly introducing some advanced concepts that you could potentially run across in developing an ASP.NET application.  I've saved it for later reference.  Overall, this tutorial was pretty good; it taught me concepts that I did not know without getting too difficult to follow.  I'm definitely ready to start on my own app now.  Tomorrow I will create my data model.  I think that I will not worry about authentication quite yet.  That was taking up a lot of time; I want to make some progress on the core functionality of the app, and then I can go in and add authorization later.

**Link to work:** <br>
[Contoso University](https://github.com/delsuckahh/Contoso-University) <br>
[Tutorial](https://docs.microsoft.com/en-us/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application)<br>
[More Tutorials](https://docs.microsoft.com/en-us/aspnet/mvc/overview/getting-started/mvc-learning-sequence)

### Day 20: February 11, 2019

**Today's Progress**: Finished 2 sections in the 'Contoso University' tutorial by Microsoft.

**Thoughts:** Got through two sections tonight, one on data concurrency and the other on implementing inheritance.  The concurrency tutorial was good to think about for applications where users might be updating the same record at the same time.  If that is a concern, and one that would cause issues for simply overwriting the data, there are some nice built in functions in the entity framework.  The inheritance section was neat because I had never seen inheritance in the context of databases.  I guess it makes sense, though, since the code first approach uses classes to create the database.  That is definitely something I'll need to keep in mind for my project.  I've only got one more section in this tutorial, and I'm ready to be done.  I'm ready to start working on my project!

**Link to work:** <br>
[Contoso University](https://github.com/delsuckahh/Contoso-University) <br>
[Tutorial](https://docs.microsoft.com/en-us/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application)<br>


### Day 19: February 10, 2019

**Today's Progress**: One more section in the 'Contoso University' tutorial by Microsoft completed.

**Thoughts:** I learned a bit more about async programming with ASP.NET today.  It's a way to free up threads when waiting for an I/O operation, which is especially helpful for high volume web applications.  Without it, each operation would need to complete before freeing up the resource for the next request.  Only a few more sections left in this tutorial.

**Link to work:** <br>
[Contoso University](https://github.com/delsuckahh/Contoso-University) <br>
[Tutorial](https://docs.microsoft.com/en-us/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application)<br>


### Day 18: February 09, 2019

**Today's Progress**: Completed another section in the 'Contoso University' tutorial by Microsoft.

**Thoughts:** Another section of the tutorial done.  I felt like I was kind of just going through the motions on this one.  Nothing really stood out to me.  It was very similar to the previous section, in that it was just updating the controller and related views for manipulating related data.  I feel like I'm ready to move on working on my project again, but I do want to finish out this tutorial.

**Link to work:** <br>
[Contoso University](https://github.com/delsuckahh/Contoso-University) <br>
[Tutorial](https://docs.microsoft.com/en-us/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application)<br>

### Day 17: February 08, 2019

**Today's Progress**: Completed one more section in the 'Contoso University' tutorial by Microsoft.

**Thoughts:** Learned about the differences between lazy, eager, and explicit loading, and when each situation might be beneficial to performance.  Seems like the only TRUE way to tell which one is better for the program is to test and see.  My initial thought is that sounds like a lot of work, BUT this could be something after the initial product is out the door (assuming performance isn't suffering).  I also learned how to retrieve related data and create ViewModels in order to achieve this.  This will help me with my meal planning app I'm sure.

**Link to work:** <br>
[Contoso University](https://github.com/delsuckahh/Contoso-University) <br>
[Tutorial](https://docs.microsoft.com/en-us/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application)<br>

### Day 16: February 06, 2019

**Today's Progress**: Another section finished in the 'Contoso University' tutorial by Microsoft.

**Thoughts:** There are 6 sections left in this tutorial.  I hope to do more than 1 per night, but this last section was pretty long.  I'm also trying to really understand the concepts before moving on, instead of just copy/pasting code just to say I did it.  I learned about complex data modeling using code first techniques.  I found a cool plugin I'm going to play around with later call Entity Framework 6 Power Tools - this is the program used to create the data relationship diagrams in the tutorial.  This could be a neat tool to use for planning future projects.

**Link to work:** <br>
[Contoso University](https://github.com/delsuckahh/Contoso-University) <br>
[Tutorial](https://docs.microsoft.com/en-us/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-a-more-complex-data-model-for-an-asp-net-mvc-application)<br>


### Day 15: February 05, 2019

**Today's Progress**: Just finished another section in the 'Contoso University' tutorial by Microsoft.

**Thoughts:** Had to do a short session tonight, my wife's brother just had a baby!  We spent some time up at the hospital so my coding time was cut a little short.  Today I learned about code first migrations and it's benefit in a production environment.  Migrations allow you to make changes to the data model and update the database without dropping and readding.  This is especially helpful in production environments so you don't lose any data.  

**Link to work:** <br>
[Contoso University](https://github.com/delsuckahh/Contoso-University) <br>
[Tutorial](https://docs.microsoft.com/en-us/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application)<br>

### Day 14: February 04, 2019

**Today's Progress**: Finished another section in the 'Contoso University' tutorial by Microsoft.

**Thoughts:** This tutorial series is going well.  I'm learning more about best practices and some behind-the-scene concepts than I thought I would.  I do wish that the tutorial would go more into detail about the code being written; it kind of glosses over the code and gives more broad information.  I did venture from the tutorial to learn a little more about interfaces.  I found a cool video that described interfaces as being loosely coupled.  The analogy given was a chef and a restaurant.  The restaraunt obviously needs a chef, but if the chef they have now decides to move on, they can just hire another chef.  This an example of a loosely coupled relationship.  A tightly coupled relationship would be a restaraunt that needs a chef named John.  

**Link to work:** <br>
[Contoso University](https://github.com/delsuckahh/Contoso-University) <br>
[Tutorial](https://docs.microsoft.com/en-us/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application)<br>
[Interface Video](https://www.youtube.com/watch?v=aQ8YkJrAbzE)

### Day 13: February 03, 2019

**Today's Progress**: Finished 2 sections in the 'Contoso University' tutorial by Microsoft.

**Thoughts:** I've decided to step away from my recipe meal planner app for a moment.  I wasn't making any headway on an issue I was facing, so I've decided to revisit a tutorial that I started but did not finish.  The tutorial is going well, it's mainly showing me best practices for designing web applications, in regards to handling requests and data security.  I also learned some neat c# tricks like the null-coalescing operator.

**Link to work:** <br>
[Contoso University](https://github.com/delsuckahh/Contoso-University) <br>
[Tutorial](https://docs.microsoft.com/en-us/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application)

### Day 12: February 02, 2019

**Today's Progress**: Helped others on discord and read up on (more) documentation.

**Thoughts:** I missed yesterday due to my wife's birthday.  I intended to still get my hour of coding in, but we went out after I got home from work, and we didn't get back until 12:30-1am.  I'll not count yesterday and add an additional day on the end of my challenge (per the rules). I've been trying to be more active on the Discord with helping and encouraging others taking part of the challenge.  I'm in a bit of a slump with my project, but hopefully I can make a breakthrough soon.

**Link to work:** <br>
[DB Practice](https://github.com/delsuckahh/data-relation-practice)<br>
[Discord](https://discord.gg/96kYFv)

### Day 11: January 31, 2019

**Today's Progress**: Not much.

**Thoughts:** This seems so simple, I'm getting a little frustrated that I can't figure it out.  I'm going to take a step back tomorrow and approach from a different angle.  Just read up on documentation and stack overflow posts, and tried a million different little solutions (none worked).

**Link to work:** <br>
[DB Practice](https://github.com/delsuckahh/data-relation-practice)<br>
[Separate User from ApplicationUser](https://msdn.microsoft.com/en-us/magazine/dn818488.aspx) <br>
[Assign User in Controller](https://gavilan.blog/2018/04/15/relationship-between-tables-and-aspnetusers/)

### Day 10: January 30, 2019

**Today's Progress**: Continued to work through linking the recipe model to the built in Identity library.

**Thoughts:** I feel like I've got the right idea in linking the recipe to the user - I'm think I'm close to getting it.  But I just can't quite get it to work.  I'm now getting an ```InvalidOperationException: Unable to resolve service for type``` error.  I think I need to add something to the Startup.cs class under the ConfigureServices method, but I can't figure out WHAT exactly.  I'll keep digging.

**Link to work:** <br>
[DB Practice](https://github.com/delsuckahh/data-relation-practice)<br>
[Separate User from ApplicationUser](https://msdn.microsoft.com/en-us/magazine/dn818488.aspx) <br>
[Assign User in Controller](https://gavilan.blog/2018/04/15/relationship-between-tables-and-aspnetusers/)

### Day 9: January 29, 2019

**Today's Progress**: Finalized recipe model on paper, fiddled around with building the database using the code first method of the Entity Framework Core. 

**Thoughts:** I made some headway in understanding the code first method of datbase design in EFC.  I'm struggling right now with making the relations between tables actually work.  I've got everything planned out, and I'm sure I could write this all out in PL/SQL...but that's not the point of this project.  I seem to have the recipe table linked to the user table, but because the "user" table is from asp.net's Identity library, it's a bit more difficult to work with and understand.  I'm trying to figure out how to automatically get the current user and assign that to the recipe table upon creation.

**Link to work:** <br>
[DB Practice](https://github.com/delsuckahh/data-relation-practice)<br>

### Day 8: January 28, 2019

**Today's Progress**: Got stuck on revising the recipe model, completed part 1 of data model tutorial. 

**Thoughts:** I was feeling good with the progress I made in the past week (and I still am), but I realized that I need to get a little more complicated.  The tutorials I went through had implemented simple data models, but I need a "complex" data model for my recipe class.  I'll spend the next day or two in tutorials, and then its back to project work.

**Link to work:** <br>
[Contoso University](https://github.com/delsuckahh/Contoso-University)<br>
[Tutorial](https://docs.microsoft.com/en-us/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application)

### Day 7: January 27, 2019

**Today's Progress**: Got a working version of the recipe model, implemented the controller/view, and updated the EFCore database to recognize the new recipe model.   

**Thoughts:** I'm still not sure what's going on in the Identity library from Day 6, but I decided to move on for now and will continue researching at a later time.  I'm feeling good about the Recipe model I created, and my next steps are more front-end in nature.  I took care of the back-end work today with setting up the model and controller, but I need to modify the view to suit my needs.
EDIT: I found through some searching on Reddit that you can scaffold out the Identity library.  This reveals all of the views that I thought were missing, which is really helpful to see.  I still am not 100% on how the controller works.  The scaffold created a IdentityHostingStartup.cs, which is the closest thing to a controller I could find.  I still don't see where it's interpreting the URL and telling the program which view to serve.

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
