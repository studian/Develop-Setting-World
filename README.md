# hello-world
sample

# < upload master >

git init

git add .

git commit -m "first commit"

git remote add origin https://github.com/studian/test.git

git push -u origin master


# < upload branch >
git init

git add .

git commit -m "first commit"

git branch v0.1             # v0.1 : new branch name

git checkout v0.1

git branch                  # show branch list

git remote add origin https://github.com/studian/test.git

git push -u origin v0.1


