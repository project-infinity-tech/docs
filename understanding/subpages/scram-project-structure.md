---
title: "Scram Project Structure"
---

# Scram Project Structure

A project in Scram is like a folder containing quite a few of the elements that make up a web app or a web site. At first it can look a little overwhelming as it isn’t like many tools that “build a website” where you are starting off…just building the website.

The good news is that you don’t need all of the elements of project to start with, and you can start with a simple template to “just build a website”.

Let’s look at them all at a high level.

# Frontend

### Apps

An Scram App is the thing you want to build. That might be a website like a marketing page. It might be a more interactive Web App like a job board. It might be a mobile app that you want to publish to an App Store. It might even be a browser plugin.

Your project can just have a single App, or it can have multiple Apps. So you could have a Web App, a simpler Mobile App, and another App for Admin users. 

All your Scram Apps in a project share a lot of the same resources that we will talk about next.

But what this means is that you can build many Apps, and have the looks similar, use similar components, and access the same data.  This will make app building faster, as you don’t need to start from scratch each time.

But of course you can still just have one app if you want!

## Theme

A project has a Theme that determines the initial look of all your Apps. It covers Typography (fonts), Colours, Icons, Spacing and everything that determines how your site looks.

## Components

Scram components are the building blocks of your app. They are the Input Fields, the Icons, the Headings and the Buttons that make up what we see on the internet. 

However, Scram also provides high level components that let you really quickly build pages that look great - and will look great in your chosen theme as well. 

Need a simple “hero” section on your main page, with an image, some text, and a form to allow people to sign up? Instead of building this up from multiple smaller components, you can choose from a range of Scram Hero Sections.

And of course you can build your own Components too, either by modifying the Scram supplied ones, or starting with a blank canvas. 

# Backend ☁️

## Database 💽

The Scram database..

## Filestore 📁

## Data Sources 🔌

In Scram, a Data Source is anything that can bring data into your Project’s App, or send it out.

OK, this might seem a little scary at first, but at its simplest this is just your internal database. And also this is where you might set up an API to get some data from an external system. 

Yes, it can get quite complex, but for now just think of Data Sources as being your database, APIs and where you might store files. 

All the Apps in a Project can access the same Data Sources. This means you only need to set up your database, or your API once. 

## Users 👥

## Server Logs 🗒️

### Data Types