---
layout: post
title:  "Create a Personal Website"
---
My High Level Plan: Host a personal website on a custom domain using GitHub pages

### Issue 1: Which static site generator should I use?
Solution: My options were Statiq, Jekyll, Gatsby. Having good expertise with .NET, I desired to use Statiq. The Lord had told me by The Holy Spirit to use Jekyll. He reminded me of how He gave me desire much earlier to learn the fundamentals of programming, and while I learnt this with C#. The Lord says this is an opportunity to be well versed in stewarding an ICT firm through exercising these skills in unique projects. Jekyll it is.

## Task 1: Setup Github pages

1. Create GitHub pages repository
	+	Click new
	+	username.github.io
2. Clone locally
3. git clone repoLink. 

### Issue 2: Whats the difference between `git clone` and `git remote add https://git-repo-url`

Solution: I see that when working with a hosted repo, it is advisable to clone it rather than create a local repo + add as a remote the hosted repo because cloning is a thorough operation ie it already handles several functionality I need but may not remember to enforce. For more details see [Difference between git clone and git remote add](https://stackoverflow.com/questions/4108778/what-is-the-difference-between-clone-and-mkdir-cd-init-remote-add-pull)

Note: This is not a tutorial, but my journey towards fulfilling a purpose. You should not directly implement these instructions, but should rather skim through the material, as you implement the official docs. 

This is useful if you face similar issues, as a guideline, to show you what to watch out for. 

## Task 2: Install Jekyll 

1.	Install Homebrew

	We will be using the jekyll official docs as the main resource alongside others

	To run commands, we will be using the Terminal application. You can find this in Launchpad > Other. I encourage you to add it to your Dock.

	You should navigate to the cloned repository

	I already have home-brew installed. You can install it (for macOS) in your terminal, using this command
	
		/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

2. Install ruby

Tip: It is advisable to use a package manager instead of brew to install ruby, so please skip this step and use rbenv

You can install ruby using homebrew using this command
		
	brew install ruby

### Issue 3: Error: ruby: no bottle available! You can try to install from source with: brew install —build-from-source ruby 

Solution: Use rbenv

Install rbenv and ruby-build using this command

	brew install rbenv ruby-build 

Info: rbenv allows me run multiple versions of ruby, ruby-build is a plugin

My systems battery ran down. I heard in my spirit, that there would be light. And ta-da! It is here! Back to work.

Integrate rbenv with your shell(bash), add this to `~/.bash_profile`
	
	echo 'if which rbenv > /dev/null; then eval "$(rbenv init -)"; fi' >> ~/.bash_profile 
	source ~/.bash_profile

Info: Forces the .bash_profile to execute. This loads the values immediately without having to reboot.

Check rbenv installation

	curl -fsSL https://github.com/rbenv/rbenv-installer/raw/master/bin/rbenv-doctor | bash 

Install required ruby version. I installed version 3.0.0 
	
	rbenv install 3.0.0 

Set installed ruby as global for rbenv 
	
	rbenv global 3.0.0

Check ruby version
	
	ruby -v

Install Jekyll and bundler gems by running the following command in your terminal
	
	gem install --user-install bundler jekyll

### Issue 4: WARNING:  You don't have /Users/mymac/.local/share/gem/ruby/3.0.0/bin in your PATH, gem executables will not run. 

Solution: Add to path by

	export PATH=“~/.local/share/gem/ruby/3.0.0/bin:$PATH"

Solution: rbenv was not initialised yet. 

Install Jekyll and bundler gems

	gem install --user-install bundler jekyll

SUCCESS!

Create new Jekyll site which overwrites the existing(in this case empty) repo

	bundle exec jekyll new . --force

### Issue 5: Could not locate Gemfile or .bundle/ directory

Solution: View current gh-pages jekyll versions here https://pages.github.com/versions/, as at the time of writing, it is 3.9.0 and run 

	jekyll 3.9.0 new .

### Issue 6: fatal: 'jekyll 3.9.0' could not be found. You may need to install the jekyll-3.9.0 gem or a related gem to be able to use this subcommand.

Solution: I searched for how to install a particular jekyll version. This is the command I saw. Run this command

	gem install jekyll -v 3.9.0

Run

	gem list jekyll

Shows the list of jekyll installed which in this case are two. The first one being the most recent jekyll version installed with the first command, and the second one been the Github pages supported jekyll version installed via the above command

Run 

	jekyll 3.9.0 new .

### Issue 6:  fatal: 'jekyll 3.9.0' could not be found. You may need to install the jekyll-3.9.0 gem or a related gem to be able to use this subcommand.

Solution: running

	which jekyll

returned 

	/Users/mymac/.local/share/gem/ruby/3.0.0/bin/jekyll

This means that the changes to the PATH variable had not reflected yet on the system, as it is meant to use the jekyll installed by rbenv. So run

	source ~/.bash_profile

running 

	which jekyll 

now shows

	/Users/mymac/.rbenv/shims/jekyll

Rerun the command to install new jekyll site in current directory

Emptied my bash_profile by this command which opened it in textedit

	touch ~/.bash_profile; open ~/.bash_profile

Contents I removed

	if which rbenv > /dev/null; then eval "$(rbenv init -)"; fi
	export PATH="$HOME/.gem/ruby/3.0.0/bin:$PATH"

Now running

	which ruby

returns

	usr/bin/ruby

Now running

	which gem

returns

	usr/bin/gem

Solution: I have to append the following to the bash_profile

	eval "$(rbenv init -)"

I run this

	touch ~/.bash_profile; open ~/.bash_profile

Which opens my bash_profile, and I append the command to integrate rbenv with the shell

SUCCESS!

Now running

	which ruby

returns

	/User/mymac/.rbenv/shims/ruby

Now running

	which gem

returns

	/User/mymac/.rbenv/shims/gem

However, running

	jekyll 3.9.0 new .

Still fails

Solution: append an underscore character before and after the version number ie

	jekyll _3.9.0_ new .

SUCCESS!

Running

	bundle info jekyll

Shows the installed jekyll

Info: It is important to either restart the terminal when edits are made to bash_profile or to force changes to it to reflect by running 

	source ~/.bash_profile

## Task 3: Setup local jekyll site for GitHub pages
Open the jekyll directory in your favourite code editor, enter into the Gemfile

comment the jekyll gem

uncomment the ghpages gem, and add the github-pages dependency version, which in my case is 212. 

You can check the current dependency version at https://pages.github.com/versions/

In Terminal, run 

	bundle update

Running the following command

	bundle exec jekyll serve --livereload

### Issue 7: require': cannot load such file -- webrick (LoadError)

Solution: run the following command

	bundle add webrick

Now running

	bundle exec jekyll serve --livereload 

WORKS!

Now you need to, push your changes to your remote repo

If you cloned the existing repo, run this in your terminal

	git push origin master

If you initialized an empty repo locally, run this

	git remote add origin https://github.com/USER/REPOSITORY.git
	git push -u origin BRANCH

BRANCH indicates the branch you want to push. -u sets the upstream 

### Issue 8: I signed commits with a wrong username and email

I noticed I was signed into a different GitHub account, I want to change the git username and email for the logs into my github username and noreply email

In my case, I wanted to change these details to the root(initial) commit

Solution: found a solution on stackoverflow via interactive rebase [Change commit author](https://stackoverflow.com/questions/3042437/how-to-change-the-commit-author-for-one-specific-commit)

## Task 4: Create a first post

To create a blog post. I have to be familiar with markdown.
Markdown resource: [Markdown](https://daringfireball.net/projects/markdown/)

By default, you are on the “Main” tab, I encourage reading the “Introduction” section. You might go ahead and skim through.
Then go to the “Basic” tab

## Summary: creating the personal website involves the following

+   Creating a git repository on Github using your Github username
+   Installing Jekyll (brew, ruby, rbenv, jekyll gem, bundler gem, webrick gem)
+   Cloning the new Jekyll project to the created git repository
+   Creating a post using Markdown
+   Connecting the domain name records of your custom domain to your Github repository

## Learnings:
+   Changing the bash profile
+   Git interactive rebase
+   Verifying package installations
+   Markdown atx-style header, paragraphs, ordered & unordered lists, indented lists, line breaks, code block, inline code, inline link

## Further steps:
In a new journey, I will add several important functionality via jekyll plugins and design a theme for this website
