npm set-script prepare "husky install"
npm run prepare

# add a hook
npx husky add .husky/pre-commit "npm run test:unit"
git add .husky/pre-commit

# make a commit
git commit -am "Keep calm and commit"
## `npm test` will run every time
