# Trust Power's Amplify Fork
> What is going on, and how do I move things forward

## Setting your environment up

```bash
(master) $ git remote add upstream git@github.com:aws-amplify/amplify-js.git
(master) $ git remote -v 
(master) $ git fetch --all
Fetching origin
Fetching upstream
(master) $ git remote -v
origin	git@github.com:navetas-loop/amplify-js.git (fetch)
origin	git@github.com:navetas-loop/amplify-js.git (push)
upstream	git@github.com:aws-amplify/amplify-js.git (fetch)
upstream	git@github.com:aws-amplify/amplify-js.git (push)
```

## Updating to match `upsteam` a.k.a the original Amazon project

1. Fetch for all remotes:

```bash
(master) $ git fetch --alll
Fetching origin
Fetching upstream
(master) $ git merge upsteam/master
```

Note: you will probably have to resolve conflicts


## Adding a 3rd part PR

```bash
(master) $ git fetch --all
(master) $ git add remote pushfix git@github.com:zegates/amplify-js.git
(master) $ git fetch pushfix
```

I'd suggest rebasing the PR on the original Amplify project's HEAD:

```bash
(master) $ git checkout -B master-aws upstream/master && git pull
(master-aws) $ git checkout -B master-pushfix pushfix/master && git pull
(master-pushfix) $ git rebase master-aws
```

You'll probably have some conflicts to resolve. 

| *OPTIONAL STEP:* |
| ---------------- |
| If you can clean things up to reduce the size of the commit (adding lots of commits will lead to you having to resolve conflicts, unless you've enabled RERERE). |
| `(maser-pushfix) $ git rebase -i master-aws` |

Once that's done merge the change in:

```bash
(master) $ git merge pushfix/master
```

```bash
(master-pushfix) $ git checkout master
(master) $ git merge master-pushfix
```

Cleanup and push with the added PR:

```bash
(master) $ git remote remove pushfix
(master) $ git branch -D master-pushfix
(master) $ git push
```
