

echo "This program reset the origin repository from gitee to github."

remote=$(git status && echo $(git remote -v | grep fetch | sed -E 's/.*(http[s][^ ]*).*/\1/') || echo "Not a git repo")

if [[ $remote == "Not a git repo" ]]; then
    echo "!! Not a git repo, exit..."
    exit 1
fi

remote=$(echo $remote | sed -E 's/.*(http[s][^ ]*)$/\1/')
remote=$(echo $remote | sed -E 's/gitee/github/')

git remote remove origin
git remote add origin $remote

echo "Done."
