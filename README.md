# frontenddot
Frontend Dot blog

## LOCAL GIT: Setup WoedPress with GitHub and local server

 1. Create **repo** on GitHub. Choose `Wordpress` gitignore file.

 2. Store your files in separate dir, eg. /home/user/git/
`git clone git@github.com:easingthemes/frontenddot.git`

 3. Symlink to local server: eg. /opt/lampp/htdocs/
`ln -s /home/user/git/blog/ /opt/lampp/htdocs/`

In `htdocs` now you have directory `blog`, 
which is something like a clone of `/home/user/git/blog/` dir.

 4. Install WordPress
Put files in `blog` dir. Create DB.  

 5. Push to Github
```
git add .
git commit -m "WP init"
git push
```

## REMOTE GIT:
 
 1. Create subdomain for blog
`blog.domain.com`

 2. Create remote git `git/blog.git`

```
cd git mkdir blog.git && cd blog.git 
git init --bare
```
 3. Create post-receive hook file

`cat > ~/git/blog.git/hooks/post-receive`

 4. Paste content

```
#!/bin/sh
git --work-tree=/home/drafil/blog.frontenddot.com --git-dir=/home/drafil/git/blog.git checkout -f
```
 - press control-d to save the file

 5. activate hook

`chmod +x ~/git/blog.git/hooks/post-receive`

!!!!!
 I had some problems with ssh to Dreamhost, so I prepared git manually with Filezilla:
 - create folder `blog.git`
 - reate bare git: `git init --bare`
 - create post-receive file in `blog.git/hook`
 - Add content to hook file:
 - Change permission to 777
!!!!!

 6. Push to Dreamhost

```
git remote add dreamhost ssh://drafil@frontenddot.com/~/git/blog.git 
git push dreamhost master
```

 7. Install WordPress, create DB

 ##GIT OVERVIEW
 1. DEVELOPMENT: Local WordPress installation with local git
 2. PRODUCTION: Remote WordPress installation with remote git - `dreamhost`
 3. Remote public git on GitHub - `origin`