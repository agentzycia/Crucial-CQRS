# Crucial CQRS

A WebAPI, Entity Framework, AngularJS (and ~~soon~~ now SignalR) sample project to demonstrate CQRS and Event Sourcing. 

Inspiration and adapation of code from:
- http://prodinner.codeplex.com/
- http://www.codeproject.com/Articles/555855/Introduction-to-CQRS
- http://www.asp.net/signalr/overview/getting-started/tutorial-server-broadcast-with-signalr
- http://blogs.msdn.com/b/mrtechnocal/archive/2014/03/16/asynchronous-repositories.aspx
- http://henriquat.re/server-integration/signalr/integrateWithSignalRHubs.html

## Components
- [SignalR](http://signalr.net/)
- AngularJS (with [Angular Material Design](https://material.angularjs.org/) )
- [ValueInjector](http://valueinjecter.codeplex.com/)
- EntityFramework 6 (Code first with adapted [Reverse POCO generator](https://visualstudiogallery.msdn.microsoft.com/ee4fcff9-0c4c-4179-afd9-7a2fb90f5838) testing using fake Context  provided by [Effort](https://effort.codeplex.com/))
- WebAPI
- [StructureMap](http://docs.structuremap.net/)
- [NUnit](http://www.nunit.org/)
- [Angular Material Icons](https://klarsys.github.io/angular-material-icons/) with [SVG Morpheus](https://github.com/alexk111/SVG-Morpheus)
- [Moment.js](http://momentjs.com/)

## Points of Interest
- Query database is recreated from Event Store on every application load (see `.API/global.asax.cs` for details)
- UI is notified of events via SignalR, not directly via UI interactions (try experimenting with multiple browser windows)
- Snapshots (Mementos) are generated and stored in the Event Store so replaying from last snapshot is faster than from entire history 

##Architecture
![CQRS Diagram](Crucial-CQRS.png?raw=true "Crucial CQRS Diagram")

## Getting started

- Install node.js & npm package manager (https://nodejs.org/download/)
- `cd ./Web`
- `npm install -g bower`
- `bower install`

### Update connection strings in `./API/web.config`
Databases will be created automatically as long as the connection string database server and credentials are correct

### Run
Pressing play in Visual Studio should start the Web [http://localhost:6307](http://localhost:6307) project and the API project [http://localhost:41194](http://localhost:41194)

### Grunt (Optional)
You can also optionally run the web project from the Web folder if you install grunt:
- `npm install -g grunt-cli`
- `npm install grunt`
- `npm install grunt-contrib-connect --save-dev`
You can then run `grunt connect` to view [http://localhost:8000](http://localhost:8000)

## Roadmap
- ~~Diagrams explaining architecture~~
- ~~Make all calls to WebAPI async and write to Event Bus asynchronously~~
- ~~Implement [Asynchronous Entity Framework repositories](http://blogs.msdn.com/b/mrtechnocal/archive/2014/03/16/asynchronous-repositories.aspx)~~
- Implement [Hangfire](http://hangfire.io/) to pick up items from Event Bus
- Restore query database form latest snapshot instead of replay entire event history
- More test coverage (using [Seleno](http://docs.teststack.net/seleno/index.html))
- More complex examples of aggregates
- Remove dependency for UI to keep track of versions
- Gracefully handle version clashes (Concurrency exceptions)

## License

The MIT License (MIT)

Copyright (c) 2015 Andy Hoyle

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
