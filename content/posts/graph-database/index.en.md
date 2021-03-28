---
title: "Graph Database"
date: 2021-03-11T11:07:29+05:30
lastmod: ""
draft: false
categories: ["Graph", "database", "GraphDatabase"]
tags: ["Graph", "database", "GraphDatabase", "model"]
resources:
  - name: "featured-image"
    src: "featured-image.jpg"
lightgallery: true
---

Image source [pixabay](https://pixabay.com/illustrations/communication-digital-computer-4871245/) by [thedigitalartist-202249](https://pixabay.com/users/thedigitalartist-202249/)

## What is a graph database?

There are many type of databases available in the market and they differ by the way it stores and operate data. Most of us would have heard or used some sort of Relational database, NoSQL or Schemaless database, Key-value database etc.

{{< admonition type=note title="Note">}}

With the advent of social networks and IoT, there is tremendous growth in degree of connected data.

{{< /admonition >}}

What do we mean by connected data, is this same as relational data? To some extent but the distinction lies in the number of connections or relations between the data and any data can be connected to each other with high degree. This way of representation of data is usually referred to as `Graph` in computer science. `Graph database are type of database where the underlying data is organised as Graph`

Data has become so essential that it is part of our lives. Everybody uses data in some form, starting from smart watches for monitoring activities to self driving cars communicating to each other, from supply chain to space satellites. Now to capture the connections between these complex data as seen in real world, graph database (graphs) provide a better way to organise, store and operate these highly connected or network data.

{{< admonition type=note title="Note">}}

A key concept of the system is the graph. The graph relates the data items in the store to a collection of nodes and edges, the edges representing the relationships between the nodes. The relationships allow data in the store to be linked together directly and, in many cases, retrieved with one operation. Graph databases hold the relationships between data as a priority. Querying relationships is fast because they are perpetually stored in the database. Relationships can be intuitively visualized using graph databases, making them useful for heavily inter-connected data. [source - wikipedia](https://en.wikipedia.org/wiki/Graph_database#:~:text=A%20key%20concept%20of%20the,the%20relationships%20between%20the%20nodes.&text=Graph%20databases%20hold%20the%20relationships%20between%20data%20as%20a%20priority.)

{{< /admonition >}}

## Data model

Lets understand how data is modeled in a Graph database, data entities are nodes in a graph and the relationships between these nodes are edges in the graphs. Any type of data entities can be represented as node and can have relationship (edge) with any other node in the database. Properties of entity are treated as properties of the node and properties of the relationship are treated as properties of edge. When we model data this way as nodes and edges, we can apply graph algorithms to find better insights which are usually unknown or hidden to other type of databases.

### TODO - model a real world data using graph
