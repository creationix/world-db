# World-DB

This is a specialized tilemap database used by a MMO game demo I'm working on.

## Design

The API is a simple key/value system with special characteristics.

 - You can only have 256 unique objects in the database.
 - every instance can exist any number of times with x,y,z coordinates.
 - 1mb planes (1024x1024x1) are allocated dynamically for infinite mapping.
 - The entire database is saved at once in atomic writes.
 - Saves are throttled to not happen more than a certain interval.
 - SIGINT and SIGTERM are caught and the data is flushed before exiting.

## Usage

The public api is very simple:

    // load the library
    var WorldDB = require('world-db');
    
    // Load or create a library with 1024x1024 planes and save throttling
    // to no more than once each every 10 seconds.
    var myworld = WorldDB('world.db', 1024, 10000);
    
    // Objects can be anything, but can't be more than 256 of them.
    var water = {name:"Water", props:[]};
    var tree = {name:"tree", hp: 43};
    
    // Set some objects
    myworld.set(0, 2, 0, wall);
    myworld.set(0, 3, 1, water);
    
    // String are singletons and can use the literals inline
    myworld.set(0, 3, 1, "wall");
    
    // Loading stuff back
    var value = myworld(0, 3, 1); // "wall"

## Contributing / Issues

If anyone wants to use this, then let me know your interest. Till then I'm going to assume it's only used by me.

## MIT License

Copyright (c) 2010 Tim Caswell <tim@creationix.com>

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in
all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
THE SOFTWARE.
