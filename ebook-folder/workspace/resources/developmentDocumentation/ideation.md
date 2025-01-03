# EBOOK Ideation

Use this space to record thoughts for future updates and ways to improve the curriculum. Includes links, examples, and bullets with date and name, please.

## updates

* Why does day 3 cover the same concepts as Day 1 and 2? could we teach the mindset of React better and progress to Routes sooner?

* in 211 or 411 teach what the PATH and SHIMS are: https://github.com/rbenv/rbenv

## Quotes

*If it's important enough to you you'll get it done.*



## Develop

Scuba stress - https://www.youtube.com/watch?v=d7M8STBlfRs


<!-- 

GCP migrate to AWS work around

https://www.notion.so/Connect-MySQL-workbench-to-AWS-RDS-Free-tier-a95068f5d6b84383ac0af2fd7bfe15f6

[Connect MySQL workbench to AWS RDS Free tier](https://www.notion.so/Connect-MySQL-workbench-to-AWS-RDS-Free-tier-a95068f5d6b84383ac0af2fd7bfe15f6)

Requirements

1. AWS Account 
2. MySQL Database admin tool

You can install the [community MySQL workbench](https://dev.mysql.com/downloads/mysql/) at the link provided.  This tutorial assumes that you have MySQL community workbench already installed and an AWS account already created. If you don't have an AWS account setup, you can do so [here](https://aws.amazon.com/resources/create-account/).

You will need a credit card to create your AWS account but we will be using a `FREE TIER` database that gives us a 12 month free trial as long as we stay within its bounds.

**STEP 1: Instantiating a AWS RDS**

From your AWS console, search `RDS`, which stands for Relational Database 
Service.  Then Click on the link.

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/c130f7c8-0dd4-4f7c-8113-eccf84ab679b/Screen_Shot_2021-01-20_at_7.15.18_PM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/c130f7c8-0dd4-4f7c-8113-eccf84ab679b/Screen_Shot_2021-01-20_at_7.15.18_PM.png)

Next, in the side `Nav` on the left hand side.  Find the link for `databases` and click on it.

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/7a3a60e6-b71a-44b6-910e-4934d7921cfe/Screen_Shot_2021-01-20_at_7.16.37_PM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/7a3a60e6-b71a-44b6-910e-4934d7921cfe/Screen_Shot_2021-01-20_at_7.16.37_PM.png)

We should then see an empty table with a button that says `create database`.  Click on it to create a new RDS database instance.

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/e8ef2932-0ed6-45c6-a68e-af2f5b442730/Screen_Shot_2021-01-20_at_7.17.57_PM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/e8ef2932-0ed6-45c6-a68e-af2f5b442730/Screen_Shot_2021-01-20_at_7.17.57_PM.png)

We should now see something like the following.

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/a4356a94-6556-4a77-8e41-5ba642513c3c/Screen_Shot_2021-01-20_at_7.18.26_PM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/a4356a94-6556-4a77-8e41-5ba642513c3c/Screen_Shot_2021-01-20_at_7.18.26_PM.png)

Keep standard create selected. Then under engine options, choose MySQL 

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/a4956c9f-da3c-4aa9-ad32-0f5ccde2373d/Screen_Shot_2021-01-20_at_7.19.59_PM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/a4956c9f-da3c-4aa9-ad32-0f5ccde2373d/Screen_Shot_2021-01-20_at_7.19.59_PM.png)

Under the template section, select `Free tier`.

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/be597500-c553-43b7-a586-40739ee375df/Screen_Shot_2021-01-20_at_7.20.49_PM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/be597500-c553-43b7-a586-40739ee375df/Screen_Shot_2021-01-20_at_7.20.49_PM.png)

Under the settings sections:

- Name your DB Instance (This will be used as your connection name in MySQL workbench).
- Give you app a username (for now, let's keep it as the default `admin`).
- Give your app a master password (Be sure to remember this as we will be using it later).

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/3a483bdb-bae0-4078-9a86-5e24f18ecb4f/Screen_Shot_2021-01-20_at_7.21.22_PM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/3a483bdb-bae0-4078-9a86-5e24f18ecb4f/Screen_Shot_2021-01-20_at_7.21.22_PM.png)

Under DB instance size, make surer that `db.t2.micro` is selected.

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/b585a73e-6f85-45a9-afa1-1a34be23f4c4/Screen_Shot_2021-01-20_at_7.25.45_PM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/b585a73e-6f85-45a9-afa1-1a34be23f4c4/Screen_Shot_2021-01-20_at_7.25.45_PM.png)

Under connectivity, switch `Public access` from No to Yes

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/4eb5303f-212b-4ada-996d-a5f9651dd26a/Screen_Shot_2021-01-20_at_7.27.32_PM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/4eb5303f-212b-4ada-996d-a5f9651dd26a/Screen_Shot_2021-01-20_at_7.27.32_PM.png)

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/d4a91ade-ea8e-42c6-a6ba-651c827523ec/Screen_Shot_2021-01-20_at_7.28.47_PM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/d4a91ade-ea8e-42c6-a6ba-651c827523ec/Screen_Shot_2021-01-20_at_7.28.47_PM.png)

Under `Additional configuration` , specify an initial database name.  If we don't specify one, RDS will not create a database.  Let's call it `Test`.

That's the initial setup.  At the bottom of the screen hit the button `Create database`.

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/098c19e3-d993-4722-980b-fbe08ade9b6e/Screen_Shot_2021-01-20_at_7.31.24_PM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/098c19e3-d993-4722-980b-fbe08ade9b6e/Screen_Shot_2021-01-20_at_7.31.24_PM.png)

You will now see our table populated with our new RDS instance.  Click on it and you will be shown a message that your db is being created.

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/eac40b9f-e9a2-4bb5-866b-241898a767d3/Screen_Shot_2021-01-20_at_7.32.35_PM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/eac40b9f-e9a2-4bb5-866b-241898a767d3/Screen_Shot_2021-01-20_at_7.32.35_PM.png)

Once it's finished being created we can connect it to MySQL workbench.

Open up your workbench and click to create a new connection.  Add your DB Instance Identifier as the connection name,  In our case it was `database-1`.

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/0b0430b8-3c0a-45cb-bfa3-7633a6a9221f/Screen_Shot_2021-01-20_at_7.40.06_PM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/0b0430b8-3c0a-45cb-bfa3-7633a6a9221f/Screen_Shot_2021-01-20_at_7.40.06_PM.png)

Let then add our hostname.  We can find it in our RDS instances under the `connectivity & security` section. It's labeled as `Endpoint`.

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/4d00ec75-b273-4931-9cf3-f176e6f18c5a/Screen_Shot_2021-01-20_at_7.42.06_PM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/4d00ec75-b273-4931-9cf3-f176e6f18c5a/Screen_Shot_2021-01-20_at_7.42.06_PM.png)

We can copy the entire string [`database-1.ccecjjyjhtbc.us-east-2.rds.amazonaws.com`](http://database-1.ccecjjyjhtbc.us-east-2.rds.amazonaws.com/). Then past it into our hostname input field.

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/fa5a6c90-0dc8-4dd2-b526-3111a78c0e01/Screen_Shot_2021-01-20_at_7.43.09_PM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/fa5a6c90-0dc8-4dd2-b526-3111a78c0e01/Screen_Shot_2021-01-20_at_7.43.09_PM.png)

We can add our username that we created.  I left mine as `admin` but if you named yours something different be sure to add that one.  Add in your password that you created by selecting the `Store in keychain`.  Lastly add the `initial database name` you provided into the `Default Schema` field.  In my case, it was `test`.

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/e353f6b5-bf9a-45f1-b63f-ce825f96cccc/Screen_Shot_2021-01-20_at_7.47.28_PM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/e353f6b5-bf9a-45f1-b63f-ce825f96cccc/Screen_Shot_2021-01-20_at_7.47.28_PM.png)

After our credentials are in, hit `test connection`. If everything goes right the first time you should see this:

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/a88279e9-b550-4d0e-adc7-cbdf6b408b13/Screen_Shot_2021-01-20_at_7.48.18_PM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/a88279e9-b550-4d0e-adc7-cbdf6b408b13/Screen_Shot_2021-01-20_at_7.48.18_PM.png)

If you didn't get that message and it's like you didn't we need to whitelist our IP address in our security group.  Back in our RDS Console under `connectivity & security` find the section labeled `Security` look for `VPC security groups` and click on the default link.  

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/c01ccb26-5835-44dd-9fbd-e3bc28a3e680/Screen_Shot_2021-01-20_at_7.50.44_PM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/c01ccb26-5835-44dd-9fbd-e3bc28a3e680/Screen_Shot_2021-01-20_at_7.50.44_PM.png)

This will open up our security groups

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/5a496d61-977f-4867-9141-e7ed94c87305/Screen_Shot_2021-01-20_at_7.52.08_PM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/5a496d61-977f-4867-9141-e7ed94c87305/Screen_Shot_2021-01-20_at_7.52.08_PM.png)

At the bottom look for a button labeled `Inbound rules` and click on it.

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/04c23611-a266-451a-8670-bf390b0fb2c2/Screen_Shot_2021-01-20_at_7.55.09_PM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/04c23611-a266-451a-8670-bf390b0fb2c2/Screen_Shot_2021-01-20_at_7.55.09_PM.png)

Click on `Edit inbound rules`, which will take you to a screen that looks like the following.

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/3fceb82e-a491-4f57-a750-86459bfd4872/Screen_Shot_2021-01-20_at_7.56.25_PM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/3fceb82e-a491-4f57-a750-86459bfd4872/Screen_Shot_2021-01-20_at_7.56.25_PM.png)

Look for the header labeled source and click on the dropdown. Change the value of the dropdown from `custom` to `My IP`.  Once it reads, `My IP`.  Save the rules.

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/3ecac375-c262-4332-9e45-6d5073fa286c/Screen_Shot_2021-01-20_at_7.58.34_PM.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/3ecac375-c262-4332-9e45-6d5073fa286c/Screen_Shot_2021-01-20_at_7.58.34_PM.png)

Now head back to your `MySQL` workbench and test your connection again.  This time if you didn't see your success message.  You should this time! -->