# Lab Report 4
## Mastering SSH, Vim, and Java Development Workflow
Throughout this lab, I accessed a remote server using SSH, edited files with Vim, and compiled and tested Java code. Below, I outline each step taken, including the specific key presses used to achieve the desired outcomes.
## Step 4: SSH into ieng6
Use SSH to connect to your ieng6 server, where you'll be performing your lab tasks. Replace "jjv001" when on the ieng6 server.
**Command and Key Presses:**

```
ssh jjv001@ieng6.ucsd.edu
Pressed: s s h Space j j v 0 0 1 @ i e n g 6 . u c s d . e d u <Enter>
```
![image](https://github.com/jjvsqz/cse15l-lab-reports/assets/142750464/7fe855eb-6802-4eef-a5b1-f432884aba4d)
## Step 5: Clone GitHub Repository
After successfully logging into the ieng6 server, you will clone the repository. This action clones your fork of the lab7 repository to the ieng6 server. By using the SSH protocol for cloning, you ensure a secure process that doesn't require entering your GitHub password, thanks to the SSH key you’ve already added to your GitHub account.
![image1](https://github.com/jjvsqz/cse15l-lab-reports/assets/142750464/97399432-fb00-4b88-a610-b77b105a6bf6)
This command securely connected me to the ieng6-202 server, allowing me to begin my work.

## Step 6: Navigate the Repository Directory
Once the repository is cloned, you need to navigate into the newly created directory.
![image11](https://github.com/jjvsqz/cse15l-lab-reports/assets/142750464/cf71a0ef-9c10-43d9-a661-5416aa49b597)

## Step 7: Compile and Run Java Tests
Compiling the Java files was necessary to ensure everything was in order before running the tests.
![image111](https://github.com/jjvsqz/cse15l-lab-reports/assets/142750464/a5b0cdc1-a89f-43d1-8c81-2ede362360a6)

**Command and Key Presses:**

```
java -cp .:"lib/*" org.junit.runner.JUnitCore ListExamplesTests
Pressed: j a v a Space - c p Space . : " l i b / * " Space o r g . j u n i t . r u n n e r . J U n i t C o r e Space L i s t E x a m p l e s T e s t s <Enter>
```
Run the test cases in ListExamplesTests. This step is crucial for identifying any failing tests that you'll need to fix. After running the tests, one test failed as expected, confirming the presence of an issue.

## Step 8: Edit Code with Vim and Run Fixed Java File Again
I used Vim to open the file that required changes.

**Command and Key Presses in Vim:**

```
vim ListExamples.java
Pressed: v i m Space L i s t E x a m p l e s . j a v a <Enter>
```
**Command and Key Presses in Vim:**

```
:set number <Enter> to display line numbers for easier navigation.
: 4 4 G to jump to line 44.
In which I press the arrow key 6 times to get to 1.
Then I press d over the 1 deleteing it. 
Then i to switch to insert mode and make the code change from 1 to 2.
<Esc> to return to normal mode after the changes.
:wq <Enter> to save the file and exit Vim.
```

**Command and Key Presses:**

```
javac -cp .:"lib/*" ListExamplesTests.java
Pressed: j a v a c Space - c p Space . : " l i b / * " L i s t E x a m p l e T e s t s . java <Enter>
java -cp .:"lib/*" org.junit.runner.JUnitCore ListExamplesTests
Pressed: j a v a Space - c p Space . : " l i b / * " Space o r g . j u n i t . r u n n e r . J U n i t C o r e Space L i s t E x a m p l e s T e s t s <Enter>
```
![imagee](https://github.com/jjvsqz/cse15l-lab-reports/assets/142750464/43f90763-90a0-42ab-a0e1-d1261039593b)

## Step 9: Commit and Push Changes
Lastly, I committed the changes and pushed them to the GitHub repository.

**Command and Key Presses:**

```
Copy code
git add ListExamples.java
git commit -m "Fix index variable in merge function"
git push
Pressed: g i t Space a d d Space . <Enter> to stage the changes.
Pressed: g i t Space c o m m i t Space - m Space "Fix index variable in merge function" <Enter> to commit the changes with a message.
Pressed: g i t Space p u s h Space o r i g i n Space m a i n <Enter> to push the changes to the remote repository.
```

## Conclusion:
This process not only fixed the bug but also enhanced my familiarity with essential development tools like SSH, Vim, and Git. Through these exercises, I refined my ability to navigate and manipulate files on a remote server, leveraged Vim for quick edits, and solidified my understanding of Git operations.
