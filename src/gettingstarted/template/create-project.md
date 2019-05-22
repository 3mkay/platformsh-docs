# Start with a template

## Create a new project from a template

In the previous step, you set up a free trial account with Platform.sh. Now you have access to the Platform.sh [management console](/administration/web.md). 

From here you can create projects, adjust account settings, and a lot more that you will explore throughout these Getting Started guides.

<video width="800" controls autoplay loop>
  <source src="/videos/create-project-mc.mp4" type="video/mp4">
</video>

Since you do not yet have any projects on Platform.sh, the first thing you will see when you sign in is a workflow for creating a new project.

1. **Name your project**

   Give your project a name like `My First Project` and then click `Next`.

2. **Set code base**

   Now you will be able to see the large collection of Platform.sh's supported templates. They are simple applications, but they could also be the starting place from which you could build something more interesting.

   If you are more comfortable with a particular language, click the dropdown labeled `All languages`. Select a language and the template list will update.

   Select a template and click `Next`.

3. **Plan size**

   The management console gives you the option of setting your plan size from the very beginning, but you can always upgrade your plan later on as well.

   For now, select the default `Professional Standard` plan size and click `Next`.

4. **Project region**

   The last step for setting up a new project is to configure its region.

   Select the region that most closely matches where most of your traffic will come from and click `Next`.
      
With these few selections Platform.sh will create the project and build the template in less than two minutes.

<div id = "buttons"></div>

<script>
    var navNextText = "I have created a new project with a template";
    var navButtons = {type: "navigation", prev: getPathObj("prev"), next: getPathObj("next", navNextText), div: "buttons"};
    makeButton(navButtons);
</script>
