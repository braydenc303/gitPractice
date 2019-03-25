# Git Recovery

This short walk-through will help in understanding branching as well as with recovering data that you may have lost somewhere along the way.

## Let's Take This Step by Step

1. Go to the GitHub website and create a new repository called recovery-practice

2. Click on the "Clone or Download" button, and copy the link.

3. In your terminal or bash, type:

    ```bash
    git clone link
    ```

    replacing the word link by pasting in the link copied from GitHub.

4. In your terminal or bash, type:

    ```bash
    touch readme.txt
    ```

    then open the file in vsCode by typing:

    ```bash
    code .
    ```

5. Inside the readme.txt file, add the following line:

    >Hello Git and GitHub

6. Save your changes. Then in terminal or bash, type:

    ```bash
    git add .
    ```

    followed by:

    ```bash
    git commit -m "initial commit"
    ```

7. Let's make another changed to our file. Add a blank line followed by the text:

    >This is a new line.

    Save your changes and add and commit them like so:

    ```bash
    git add .
    ```

    followed by:

    ```bash
    git commit -m "Added new line."
    ```

8. Now let's create a new branch called "another". In your terminal or bash type:

    ```bash
    git branch another
    ```

    now if you type:

    ```bash
    git branch
    ```

    You should see something like:

    ```bash
    $ git branch
      another
    * master
    ```

9. Again, add a blank line to README.txt then add:

    >This is another new line.

    Don't forget to save, add, and commit your changes.

10. Keeping vsCode up on the screen, and either uset the built in terminal, or a small terminal window on top of that so that you can see what is going on, alternate between the following commands:

    ```bash
    git checkout master

    git checkout another
    ```

    making sure that you end in the master branch.

11. Now that you are back in master, let's create a different branch and switch into it at the same time:

    ```bash
    git checkout -b different
    ```

12. Add the line:

    ```bash
    This is a different new line.
    ```

    As always, save, add and commit your changes.

13. Take a minute switching between all of your branches to get an idea of what is going on, ending back in master.

14. Let's create two more branches. While in master, type the following commands:

    ```bash
    git branch delete-me
    git branch reset-me
    ```

15. Switch into your reset-me branch. Add another blank line to your README.txt file followed by:

    >I am going to reset this branch.

    Save your changes, then add and commit them like so:

    ```bash
    git add .

    git commit -m "Getting ready to reset a branch."
    ```

16. Now to be able to reset our branch to a prior version, we need to know the SHA-1 value for a prior version. In terminal/bash, type:

    ```bash
    git log
    ```

    You should see a series of summaries of each commit with a long series of letters and numbers, this is what is referred to as an SHA-1 value, or "hash". We will need one of these in order to reset our branch to an earlier version. Luckily we don't need the whole thing.

17. Highlight and copy at least the first seven characters of the SHA-1 value associated with the Initial commit.

18. Now, type the following:

    ```bash
    git reset --hard SHA-1
    ```

    being sure to paste in the SHA-1 value that you copied.

19. Take a look at your README.txt file. You may notice something different about your file. Depending on whether or not we grabbed the right SHA-1 value. If not, you may see some of the lines of text are now gone. However, if we did grab the right one, all of the lines of text will still be displayed, but if you look closely at the tab in vsCode, there should be a message telling you that the file was deleted from disk. Either way, we need to do a little work to get our data back.

20. In your terminal/bash, type in:

    ```bash
    git log
    ```

    Notice that everything except for the initial commit is now gone. We are going to need another command to help us get things back in order.

21. Once again in terminal/bash, type:

    ```bash
    git reflog
    ```

    This time, you should see a much longer list things that Git has been keeping track of, including switching from one branch to another, along with shortened versions of the SHA-1 values. Find the one associated with the commit message "Getting ready to reset a branch." and copy the entire short SHA-1 value.

22. Now type the following command:

    ```bash
    git branch recovered-reset SHA-1
    ```

    replacing SHA-1 with the value that you copied.

23. Though you are still in the reset-me branch the command that we just ran should have created a new branch called recovered-reset. Type in:

    ```bash
    git branch
    ```

    You should now see a list of branches that includes the recovered-reset branch that we just made. Switch to that branch by typing:

    ```bash
    git checkout recovered-reset
    ```

    You should now be in the recovered-reset branch that has the lines:

    >Hello Git and GitHub
    >
    >This is a new line.
    >
    >I am going to reset this branch.

    and there should be no indication in the tabs that any files have been deleted from disk.

24. Now it is time to learn how to recover a deleted branch. Switch into your delete-me branch. Add another blank line to your README.txt file followed by:

    >I am going to delete this branch.

    Save your changes, then add and commit them like so:

    ```bash
    git add .

    git commit -m "Getting ready to delete a branch."
    ```

25. In your terminal, switch back into your master branch. Then, enter the following command:

    ```bash
    git branch -D delete-me
    ```

    Now if you type git branch, you will see that the delete-me branch is no longer listed.

26. In order to get our deleted branch back, we need to look back through our history to find it's SHA-1 value. If we were to simply use git log, we would not see it. To see everything we have done in every branch, we need a more powerful command. In your terminal/bash, type:

    ```bash
    git reflog
    ```

    Once again we see our longer list of what we have been doing in Git.

27. Scan down through the entries, and find the one next to the commit message, "Getting ready to delete a branch." then highlight and copy that SHA-1 value.

28. In terminal type:

    ```bash
    git branch recovered-delete SHA-1
    ```

    replacing SHA-1 with the value that you copied, and press enter. Now when you type git branch, you should see that we have just created a new branch called recovered-delete. Switch to that branch and you should see that once again, your README.txt file has the lines:

    >Hello Git and GitHub
    >
    >This is a new line.
    >
    >I am going to delete this branch. -->

We've covered a good bit so far. If you would like to learn more about git and a workflow that will be helpful when working in a small group setting, be sure to check out my [Centralized Workflow](https://github.com/braydenc303/GitTutorial) tutorial. Practice with this or another repo a bit, and if you'd like to learn more from people who really know what they are talking about, checkout the book "Pro Git" by Scott Chacon and Ben Straub [here](https://git-scm.com/book/en/v2).
