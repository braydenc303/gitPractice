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

8. Now let's create a new branch called "another". In your terminal or bash type:

    ```bash
    git branch another
    ```

9. Add a blank line to README.txt then add:

    >This is another new line.

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

16. While still in your terminal/bash, type in:

    ```bash
    git log
    ```

    You should see a few entries. Highlight and copy at least the first seven characters of the SHA-1 value that is associated with the commit message, "Getting ready to reset a branch."

17. Now type the following command:

    ```bash
    git branch recovered-reset SHA-1
    ```

    replacing SHA-1 with the value that you copied.

18. You should now be in a new branch called recovered-reset that has the lines:

    >Hello Git and GitHub
    >
    >This is a new line.
    >
    >I am going to reset this branch.

19. Now it is time to learn how to recover a deleted branch. Switch into your delete-me branch. Add another blank line to your README.txt file followed by:

    >I am going to delete this file.

    Save your changes, then add and commit them like so:

    ```bash
    git add .
    git commit -m "Getting ready to delete a branch."

20. In your terminal, switch back into your master branch. Then, enter the following command:

    ```bash
    git branch -D delete-me
    ```

21. In order to get our deleted branch back, we need to look back through our history to find it's SHA-1 value. If we were to simply use git log, we would not see it. To see everything we have done in every branch, we need a more powerful command. In your terminal/bash, type:

    ```bash
    git reflog
    ```

    This will display a summary of everything that you have done in this project to date, even if it was just switching between branches.

22. Scan down through the entries, and find the one next to the commit message, "Getting ready to delete a branch." then highlight and copy that SHA-1 value.

23. In terminal type:

    ```bash
    git branch recovered-delete SHA-1
    ```

    replacing SHA-1 with the value that you copied, and press enter. You should now be in a new branch called "recovered-delete" that has the lines:

    >Hello Git and GitHub
    >
    >This is a new line.
    >
    >I am going to delete this branch. -->

We've covered a good bit so far. Be sure to check out my Centralized Workflow tutorial. Practice with this or another repo a bit, and if you'd like to learn more from people who really know what they are talking about, checkout the book "Pro Git" by Scott Chacon and Ben Straub [here](https://git-scm.com/book/en/v2).
