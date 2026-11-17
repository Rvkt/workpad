---
title: "We made Cron EASY!"
source: "https://www.youtube.com/watch?v=miRQPbIJOuQ"
author:
  - "[[Supabase]]"
published: 2024-12-04
created: 2026-11-17
description: "Supabase Cron allows you to schedule and automate work ... from your database! In this video, Jon Meyers demonstrates how to enable the cron extension, use natural language to specify a schedule, and"
tags:
  - "clippings"
---
![](https://www.youtube.com/watch?v=miRQPbIJOuQ)

Supabase Cron allows you to schedule and automate work ... from your database! In this video, Jon Meyers demonstrates how to enable the cron extension, use natural language to specify a schedule, and automatically drop every row from your database! 😈  
  
✍️ Supabase Cron (blog): https://supabase.com/blog/supabase-cron  
  
00:00  
  
💻 Videos to watch next:  
▶ We improved Supabase AI ... A lot: https://youtu.be/\_fdP-aaTHgw  
▶ 3 new things you can do with SupaCharged Edge Functions: https://youtu.be/envrsJ8VfAU  
▶ Using bolt.new and Supabase to build an Instagram clone: https://youtu.be/9c4v27ZlH6Q  
  
👇 Learn more about Supabase 👇  
  
🕸 Website: https://supabase.com/  
🏁 Get started: https://app.supabase.com/  
📄 Docs: https://supabase.com/docs  
  
🔔 Subscribe for more tutorials and feature updates from Supabase: https://www.youtube.com/channel/UCNTVzV1InxHV-YR0fSajqPQ?sub\_confirmation=1  
  
📱 Connect with Us:  
🐙 Github: https://www.github.com/supabase  
💬 Discord: https://discord.supabase.com/  
🐦 Twitter: https://www.twitter.com/supabase/  
▶ Instagram (follow for memes): https://www.instagram.com/supabasecom/  
  
  
ABOUT SUPABASE:  
Supabase is the open source Firebase alternative. Supabase provides a full Postgres database for every project with pgvector, backups, realtime, and more. Add and manage email and password, passwordless, OAuth, and mobile logins to your project through a suite of identity providers and APIs.  
  
Build in a weekend, scale to millions.  
  
#Supabase #AppDevelopment #RealtimeApps #DeveloperTools

## Transcript

### Introduction to cron jobs

**0:00** · I'm going to show you how to use cron jobs to obliterate every message you have ever received in your database I'm also going to show you how to do some less destructive stuff that you might actually want to do at your job unless this is your last day in which case blow away the database what are they going to do fire you so cron jobs are a way to schedule tasks or a block of work that you want to run at a particular time this could be every 30 seconds or some maintenance task that you want to run at 3 a.m.

### Setting up the project

**0:30** · every night or maybe a yearly report that pulls together a whole bunch of data from a whole bunch of tables to show your big bosses some colorful charts with arrows pointing up and to the right and they're dead simple in the superbase dashboard so here I have a super basic project it's basically just a table for messages and we basically want to delete every Row in this table every 60 seconds so we're essentially building Snapchat but just for messages

**0:59** · so if we head over to Integrations and then look for the official Chron jobs integration I might just zoom out a little bit so we can actually see it so this allows us to schedule and automate tasks to run maintenance routines at specific intervals and to use this integration we just need to enable the PG Chron postgress extension by clicking this button and let's confirm we want to enable this extension and now we have this new Chron jobs tab where we can add a new Chron job the name of this one can be delete old messages and then we can

### Configuring the cron job

**1:32** · write a Chron expression using these stars and numbers and symbols now I don't know about you but for me the worst thing about writing cron jobs is trying to work out this magic incantation to get it to run at the right time so thankfully we have these suggestions for things that you might want to do like run every night at midnight or every 5 minutes and so you

**1:54** · could click one of these and then modify it to be what you actually want or if that's still a little confusing you can use natural language to describe when you want this schedule to happen so in this case let's say we want it to happen every 10 minutes and then we can see our Chron expression has been updated to be star/ 10 star star star star which means

**2:16** · this job will run every 10 minutes we can then choose what we actually want to do so if it's something simple we can just run an SQL snippet for something a little bit more complex we could use a postgress function or if we enable the p G Net extension we can send a HTTP request to an external service or run

**2:35** · one of our superbase Edge functions let's start with a super simple example of just running an SQL snippet so if we scroll down slightly we can see this section where we can actually write the SQL snippet we want to run every 10 minutes warning the following features SQL queries performed either by professionals or under the supervision of professionals accordingly superbase must insist that no one attempt to recreate or reenact any of the queries performed in this video so let's obliterate every message in our database by saying delete from messages but we

### Database automation execution

**3:07** · only want to do this where the created at column is less than this moment right now minus an interval of 10 minutes now I don't actually remember when I put all of these messages into the database so how about we go with a slightly longer interval of maybe 2 hours just so we can

**3:29** · see that the messages are actually there and then when this job runs they disappear so let's create this new Chron job and now we can go over to our messages and confirm that they are indeed still there our friends are having this wonderful back and forth conversation about launch week and how many tickets there are in their social feeds and so now if we go back to our Integrations and go to cron Jobs go to the cron jobs Tab and edit our Cron job

**3:56** · we'll run this one every 30 seconds just so we can see that something has actually happened and then rather than 2 hours let's make this our interval of 10 minutes and save our Cron job and now we can view our previous runs which brings us over to the SQL editor and populates it with a query to get our job Run details for this specific job so let's run this SQL snippet and we can see our job has run four times with our delete

**4:23** · command so if we head over to the table editor and look at our messages table we'll see that all of our messages have been deleted and if we insert a new message that says everything is temporary and spelled temporary correct

**4:39** · and click save we'll see we have that message but if we jump forward 30 seconds in time and refresh the page a few minutes later ah we set this to 10 minutes so if we go back over to our Cron job so go to Integrations and then cron jobs cron jobs and edit this Cron

### Advanced edge function setup

**4:58** · job so it's running everything 30 seconds but it's only deleting messages that are 10 minutes old so let's make this 1 minute just so that we don't have to change as much later a little longer than a few minutes later and now if we go back over to the table editor and look at the messages table we'll see our message is gone so let's Implement a slightly more advanced example where we have an edge function which sends an email to every user who sent more than 100 messages in our ephemeral temporary

**5:28** · messages platform so if we go over to Integrations and then cron jobs and over to the Chron jobs Tab and create a new job called email active users we want this one to run every night at midnight let's say and rather than an SQL snippet or a postgress function we want to run a super base Edge function so we need to enable the pget extension to be able to send HTTP requests to our Edge functions

**5:55** · so let's install that extension and confirm yes we want to enable this extension and now we can choose our superbase Edge functions option we can choose a method for how we want to call our Edge function so let's say a post request the edge function we want to call or send a request to is this send

### Automation use cases and wrap

**6:13** · emails to active users Edge function we can leave the timeout and headers and parameters as they are and just create our Chron job and now every night at midnight our database is going to automatically send a post request to this Edge function which will handle emailing all of the active users on our

**6:34** · platform so cron jobs are great for scheduling batches of work like sending emails or maybe sending a summary message to a slack channel for work you can use it to Archive soft deleted or

**6:49** · disabled accounts or back up your entire database and we actually use cron jobs internally at superbase to automatically pair up everyone in the company with a coffee buddy once a month now I'm not meant to tell you this because at the time of recording this video it hasn't actually been launched but there is something really cool coming that goes hand inand with cron jobs you could say our support cues have been overflowing

**7:16** · with requests for this feature so if I'm allowed to tell you about it I'll put a video right here that takes you through this awesome feature but otherwise you'll need to grab a number and head to the back of the line hint hint but until next next time keep building cool stuff