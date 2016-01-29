---
title: "Custom View Helpers"
date:   2016-01-29 17:11
categories: rails
permalink: custom_view_helpers

---

So today I'm working with view helpers for the Crowdfund app. 
View helpers are great at making the app look a lot more refined. It includes things like pluralize, truncate, time_ago_in_words and distance_of_time_in_words. They're pretty cool. 

However, it starts to get a little tricky when we want to display things that aren't included in the built in view helpers. This is where custom view helpers come in!

For example, in the Crowdfund app so far we have a field that displays the date that the pledging ends on using the distance_of_time_in_words. However, what if we wanted a conditional that specifies if that date is passed then we just want it to display "All done!". 

Well, we can easily add the conditional Date.today > pledging_ends_on to choose between whether to display the date of the "All done!" in the projects_helper, (and this does work) however this sort of logic is not a View level concern and so the codes needs to be moved around a bit. 

The Date.today > pledging_ends_on conditional by definition says whether the pleding has expired or not. As such, this is something that should live in the Model. We can define this as so:

def pledging_expired?
  Date.today > pledging_ends_on
end

This allows us to then call it in the projects_helper like before except now we have defined whether the date is expired or not in the project Model where it should be. Remember, business logic should always be expressed in the Model, the View should only be used to generate the output. This might not seem like a big deal but as an app gets larger and larger we need to make sure we are placing the code where it should be. It also means we can call the pledging_expired? method from anywhere in the app now if need be. 



