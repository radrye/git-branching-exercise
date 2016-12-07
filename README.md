# An Exercise on Branching And Working Remotely with GitHub

## Introduction

So far, you have mostly been working on a single branch of a Git repository. The single branch you have been working on is the `master` branch, which is the default branch that is created when a Git repository is initialized.

GitHub Pages is also serving your content from the `master` branch. This means any changes you push to GitHub will automatically update your users. To avoid breaking your users with bad updates, you have to test your changes locally before pushing to GitHub. Having to test your changes locally first means any pending changes can only exist on your laptop. Having your pending changes exist solely on your laptop means your changes aren't backed up and anyone reviewing your code can only do so on your laptop. This is a very restrictive working environment.

If you think of branches as workspaces, you can think of the `master` branch as the workspace you share with your users, i.e., the code you have in your `master` workspace is the code you want your users to see. Wouldn't it be nice if there were a separate workspace for yourself (or for your team)? This is what branches are for.

The purpose of this exercise is to introduce you to manging branches locally and in GitHub.

## Set Up

1. Fork this repository: git@github.com:fe-101-sea-nov-15-2016/git-branching-exercise.git

2. Configure GitHub Pages for your fork.

3. Add me (GitHub username: christopherbaek) as a collaborator.

4. Clone the repository on your laptop.

## Local Branches

### Scenario 1: Testing a Change then Discarding it

1. Check what branch you are on. You should be on `master`.

        $ git branch
        * master

2. Create a branch named `development` that will hold the changes you are testing and switch to it.

        $ git checkout -b development
        Switched to a new branch 'development'

3. Verify you are on your new `development` branch.

        $ git branch
        * development
          master

4. Make a change, such as creating an "about" page.

        $ cp -p index.html about.html

5. Check your repo status and verify you have a new, untracked file, stage your file, and create a new commit.

        $ git status
        ...
        $ git add about.html
        ...
        $ git commit -m "Create a new about page"

6. Generate a directory listing to verify your new about page exists.

        $ ls
        about.html  index.html

7. Switch to your `master` branch to verify your new file does not exist there. The file should not exist there because the `development` branch has your new changes, but the `master` branch does not.

        $ git checkout master
        Switched to branch 'master'
        $ ls
        index.html

8. Assume you took some time to think about your project and you decided you no longer want the change you made in step 4. You can simply delete your `development` branch and your `master` branch remains completely unaffected.

        $ git branch -d development

9. You should have received a warning that the changes in the `development` branch are not in the `master` branch. This is Git helping you out, but you should already be aware of this. Git should also help you out by instructing you how to delete the branch anyway.

        $ git branch -D development

### Scenario 2: Testing a Change then Keeping it

Repeat steps 1-7 from Scenario 1.

8. Assume you took some time to think about your project and you decided you want to keep your changes. Now it is time to `merge` your changes from your `development` branch to your `master` branch.

         $ git merge development

9. Verify your changes exist in your `master` branch.

         $ ls
         about.html index.html

10. Push your changes to your users.

         $ git push

## Remote Branches

### Posting a Change for Review

Repeat steps 1-7 from Scenario 1, but this time create a "contact" page instead of an "about page.

8. Switch back to your `development` branch because now you need to get these changes online for review.

        $ git checkout development
        Switched to branch 'development'

9. Push these changes to GitHub while keeping them in a separate branch.

        $ git push -u origin development

10. Go to your repo page in GitHub (i.e., in the browser) and verify there are now two branches.

11. Visit the GitHub Pages version of your project in the browser and verify your changes are not live. They should not be because GitHub Pages should be serving your site from the `master` branch, but your change is only on the `development` branch.

12. Go to your repo page in GitHub and create a Pull Request. Set the base branch as `master` and the compare branch as `development`. Create the pull reques, assign it to me, and I will be notified that your code is ready to review.

### Scenario 3: Modification Required

I may suggest changes to your pull request. In this case, all you need to do is create another commit on your `development` branch addressing my comments, and push it. The pull request will be updated to include your new commit automatically.

### Scenario 4: Approved

Once your pull request looks good, I will approve it. After approval, you can navigate to your pull request on GitHub and click the "Merge pull request" button.

Behind the scenes, this is doing the same merge you did in Scenario 2, but on GitHub.

On your laptop, switch to your `master` branch and pull the latest changes to verify GitHub has performed the merge.

        $ git checkout master
        $ git pull

## Issues

I may look at your project and see something that should be fixed. In this case, I will open an issue for your project. Each issue in GitHub is assigned an ID (e.g., #1, #7, #50).

If I open an issue and you fix it, the workflow in Scenarios 2, 3, 4 will remain the same. The only difference is that you should address the issue by its ID in your commit message so the pull request, commit, and issue all get linked together.

For example, if I open issue #7, your commit message should look something like this:

> Addressing styling from issue #7
> 
> - Updated stylesheet
> - Update page to include new stylesheet elements
> - Additional chnages to page structure

After a pull request is merged and I have verified my issue was resolved, I will close the issue.

