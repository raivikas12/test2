## Updating package.json

At the beginning of each cohort, update the versions in package.json by:

```sh
rm -r node_modules
cp package.json package.json.bak
sed -E 's/"\^.+"/"*"/' package.json.bak >package.json
npm update --save
npm update --save-dev
  # note: make sure it works
rm package.json.bak
```
- the above sed command replaces all of the versions with an `*`. Then npm updates grab the latest version and replace.

## Structure

Dependencies are stored in [`package.json`](package.json).

Do not configure `grunt` packages directly in the
[`Gruntfile.js`](Gruntfile.js). Instead, store configurations in the
[`grunt`](grunt) directory. You won't need a top-level key, since that's
generated by the `Gruntfile.js` based on the filename of the configuration
object stored in the `grunt` directory.

**Note:** developers who add link tags should be firmly reminded to follow
directions

## Linux Troubleshooting

Very rarely, `package-lock.json` can cause a problem for Linux users. If
`npm install` is failing on Linux or developers are seeing errors related to
missing dependencies or modules, they should:

```
git rm package-lock.json
rm -rf node_modules
npm install
git add package-lock.json
git commit
```