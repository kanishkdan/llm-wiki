---
layout: layouts/posts.njk
title: Building my first product from scratch
description: "In this article, I do a tell all, I go into a detailed overview of
  how I coded out a product from scratch and got to my first few customers.
  Useful for those who aren't developers but one day plan to build their own
  software. "
type: Info
date: 2024-06-30T02:13:00.000Z
---
I left my job on December 31st 2023. 

Reason? *I wanted to **learn how to code**.*

Plan? *Code and **build a product from scratch** on my own and get it to 100 paying customers.* 

The past few months have exactly been that. I'll be officially launching my product soon but before I do that, here's a quick overview of my process. For anyone aspiring to build a product of their own, this is for you. I’ll go deep into what my tech stack was, how I approached building things and what the journey has been like - a tell all. 

### Some key points

* AI is your best friend, use it. It’d have taken me 2X the amount of time without it. I currently use Anthropic's [claude](https://claude.ai/) models. 
* Don’t solely trust AI. Couple it with stack overflow, reddit, docs etc. The world has solutions for every problem you face.
* You’ll face a ton of bugs. Just remember each problem is solvable. You just need to be patient and do your work.
* A few (helpful) pre-requisites before you start building your own software

  * **Learn HTML/CSS/Javascript.** Building blocks of the web. Helps you understand how the web works.
  * **Understand at least one query language.** MySQL, PostgreSQL, MongoDB. You’ll be managing data when you build an app. Being able to fetch and manipulate data is a useful skill.
  * **Learn how to interact with the terminal**. When building your app, you’ll often have to use the command line. Try and get used to it.

    * in TopHire, I’d do casual bite-sized projects to train myself to use the terminal.
    * you should be able to use the basic stuff (cd, cat, echo, sudo, nano). Bonus is to write scripts and set shortcuts for them ~ bash / zsh.
    * learn git. Almost essential to know how developers manage different version of their code.
    * learn design fundamentals. Go through [uxtoast](https://www.uxtoast.com/) to understand common design principles.

### Deciding what to build

<p class="text-slate-500 mobile:text-base text-lg">Feb to Mar, 24</p>

* Decided on an idea — a slack bot which allows you to schedule async meetings, standups and check-ins all inside slack. 
* Didn't have to spend time validating the idea, similar tools already exist. 
* I decided on a tech stack.

  * Python is fairly simple to use, the syntax is easy to understand.
  * Decided to use Django for my framework. A framework adds functionalities that you would otherwise need to handle yourself. 
  * For frontend, decided on tailwind and Vanilla JS. Already used tailwind while building IndiaTechSalaries website.
  * DB was postgresql. Fairly comfortable with the syntax.
* Started with writing a PRD (pm habit). Noted down some of the major points but I realised the best way to start is writing my first lines of code. Started coding instead.
* Spent the first couple weeks coming up with a basic landing page and trying to learn how OAuth works. 
* Came up with a static website with a google login to a dashboard. 
  ![First Week Dashboard](/static/images/blog/first_week.gif)
* Added a basic workflow creation form in Django plus started trying to understand how Slack APIs work. 
  ![First Workflow Form](/static/images/blog/first_workflow_form.jpeg)
  ![Slack API Tests](/static/images/blog/slack_api.jpeg)
* Completed the first version of the form backend on March 18. Users could now create new workflows and edit them too. It looked bad, but that didn't matter yet. 
  ![First Dashboard](/static/images/blog/first_dashboard.gif)

### First iteration of a working application

<p class="text-slate-500 mobile:text-base text-lg">Mar to May, 24</p>

* Started trying to figure how to do Slack OAuth. Slack has two flows primarily.

  1. for installing the app to a workspace — using slack oauth
  2. for logging in a user — using slack’s openid mechanism 
     Spent a ton of time getting this right (roughly 2-3 days of continuous experimentation). Recommendation — just trust slack’s docs for this, it’ll show you the right path. 
* Read a bit about concurrency. Thought if multiple workflows need to run simultaneously, concurrency was important. In hindsight it wasn’t too important (I’ll write about this in the future).
* Started building the landing page and the dashboard UI. The first iteration sucked but I liked the theming. 
  ![First Landing Page & login](/static/images/blog/first_ui_with_slack_login.gif)
* Pace was going well till now. I had a working app which,

  * allowed you to create and edit workflows, backend was set up with celery for async processing, could install apps to workspace using slack, even slack login was setup
  * had a shitty but decent landing page and dashboard layout
  * had a flow for clicking a button to update team data (updating the team’s channels, users etc.)
  * see reports of all participants on the website directly.
* decided to make this version live. Hosted it on an EC2 instance. Used nginx, gunicorn for running my app. Faced some trouble installing rabbitmq to the machine but again the rabbitmq docs helped.
* Made the most commits in a day on 2nd May (my birthday) lol. 
  ![Most Commits](/static/images/blog/most_commits.jpeg)
* Upgraded the ec2 instance from t2.micro to t2.small - wanted to improve RAM plus CPU performance.

### First customer and adding payments

<p class="text-slate-500 mobile:text-base text-lg">May to Jun, 24</p>

* Got my first customer — TopHire. Spoke to Siddharth and he recommended a trial run for the app. Started with one workflow.
* Trial run lasted a few weeks with only one bug. Fixed those and TopHire became a superuser of my both \~ presently running about 20 workflows across \~ 30 participants.
* Started thinking of how to build out payments. Attempted stripe but unfortunately stripe has exited India. Next best alternative - Razorpay. 
* Began setting up Razorpay, got help from a friend in better understanding how the payments flow works on Razorpay.
* Made improvements to the UI/UX, added a dashboard page plus analytics.
* Added a billing section with invoice management.
* Razorpay approved my account, made payments live

### Second customer, AI & going global

<p class="text-slate-500 mobile:text-base text-lg">Jun to Jul, 24 (Now)</p>

* Was thinking of how integrating AI would help. Decided to summarise participant responses and share summaries with users.
* Meanwhile, had a casual conversation with a college batchmate, pitched him the bot — he and his team found it interesting and signed up for a trial.
* **Disaster**: within minutes of them signing up they faced a bunch of errors. Fixes took me <10 minutes but I was worried about the impression it’d have on them.

  * Fixed the issues, asked them to try again. Made sure everything worked this time. It worked fine.
* Decided to use OpenAI’s GPT4. Got some api errors, their customer team was annoying to deal with.
* Switched to using gemini. A [few notes](https://www.linkedin.com/feed/update/urn:li:activity:7208361541518151680/) on why gemini apis make more sense to use, especially at an early stage.
* Made AI summaries live. The AI summaries make it much easier to extract key points and go through those.
* Added timezone management. Allowing users from all over the globe to use my software.
* Added a settings page for managing users and other settings.
* What my product looks like now. 
  ![Live App Preview](/static/images/blog/live_app.gif)

### What’s next

* Publicly announcing and launching [howsthisgoing](https://howsthisgoing.com) - will put posts on reddit, linkedin, twitter, product hunt etc.
* Getting back to building features. 
* Doing a lot more sales calls and working towards the 100 paying customers goal.
* Building in public on twitter and linkedin. 

### Current Github Stats

### ![Current Github Stats](/static/images/blog/current_github_stats.png)
