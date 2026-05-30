# mlops-bootcamp-dagshub-dvc

DVC: data version control -> remote repository for data

python library: dvc

As we do git init, we also do dvc init -> folder .dvc is created + .dvcignore file
These files will need to be added to the git remote repository

Add a data to the tracking system: dvc add data/data.txt --> this automatically adds data.txt to the INTERNAL .gitignore of the data folder, so Git doesn't track the file, it's DVC who does it
data.txt.dvc contains the hashed key of the data
In the .dvc/cache we will have the mapping hash -> content

What does git need to track? data.txt.dvc + data/.gitignore
git add data/data.txt.dvc

Once we change the data: dvc add data/data.txt + git add data/data.txt.dvc