# Billing Tags

If your project uses AWS services, please use billing tags.  

## What are billing tags?
Billing tags help organize things that cost us money.  So far, we have implemented three tags:  Project, 
Environment, and OtherProjects.  The tag names are case-sensitive.

- Project
  * This is the main project the resource serves.  For example, the BibService was created for the Discovery project.
    + We haven't settled on naming conventions for the Project tag value, but I'm using camel case for now.
    + Make sure that all resources for your project have the same "Project" tag value.  So every lambda, EC2 instance, RDS resource, ElasticBeanstalk resource, etc. that have to do with "Discovery" are labeled "Discovery", not "discovery/Dis cover/any other variation".
  
- Environment
  * Options are: "production", "qa", and "development".
  
- OtherProjects
  * Does more than one project use this resource?  Are there projects, other than the one you originally created the resource for, 
  that are reading from or posting to the resource?  For example, if I were to delete the BibService, not only would the 
  Discovery project be affected, but the MyLibraryNyc project would also suffer.  This tag is where we'll put that info. 
    + Separate the project tags with a forward slash.  Ex.:  if MyLibraryNyc and FooBar are using BibService, then the OtherProjects value would be "MyLibraryNyc/FooBar".
    Why not a comma, you say?  Because Amazon won't let us.  Why not put everything into the Project tag?  Because that'd make pivot tables cry in excel billing reports.  We're sorry.

## How do I add tags?
Go to the resource configuration page.  Scroll down -- the Tags section is about mid-page.  
Since we're trying to do configuration-as-code, please make sure to add billing tags to your .ebextensions / other configuration files.

