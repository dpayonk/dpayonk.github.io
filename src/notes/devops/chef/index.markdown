---
layout: page
title: "My notes about experiences with Chef"
date: 2013-06-05 13:52
comments: true
sharing: true
footer: true
---
I recently used [Chef](http://opscode.com/chef)
for my Amazon Cloud servers
and just wanted to document some of the random notes in case
it helps someone else.

## Commands



## Creating cookbooks

metadata.rb can describe your cookbook like a gemspec does

include_recipe 'database'
depends 'database' #depends on mysql



postgresql_database 'xsell_pre' do
  connection(
      :host      => '127.0.0.1',
      :port      => 5432,
      :username  => 'postgres',
      :password  => node['postgresql']['password']['postgres']
  )
  action :create
end

1. Moneta breaks Chef install as of 0.7.0
2. knife command broke because of AWS key
3. Installation Notes for chef omnibus
4. Loads an embedded ruby into /opt/chef
5. GEM_PATH plays vital role in chef configuration
6. Knife solo will allow me to push chef solo to new machines
7. chef configure redis is a good example

##Open Issues with AWS VPCs and my chef scripts
- When I startup a server, I don't know the IP address
- When I start up a server, I don't have a DNS record for it

