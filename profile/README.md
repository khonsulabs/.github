# What is Khonsu Labs?

Khonsu Labs is the passion-project of [@ecton][ecton]. We have a long-term goal of developing [Cosmic Verge][cosmicverge] in [Rust](https://rust-lang.org), and everything we do is open-source under both the MIT License and the Apache License 2.0.

We are not in this for money. We are here to build something unique with the community. As such, if our vision is unattainable, we would rather walk away than sell out. We promise to:

- Never offer a "cash-shop" where real money is exchanged for digital goods or any gameplay enhancing functionality.
- Be transparent with financials once we begin any form of monetization including donations.

## Interacting with us

- **Github Issues**: If you're wanting to request a feature or file an issue, we are using Github Issues to manage [our roadmap](https://roadmap.khonsulabs.com/).
- [**Discord**](https://discord.khonsulabs.com): We have a Discord server where we chat, co-work, and occasionally play games.
- [**Discourse Forums**](https://community.khonsulabs.com/): Our community forums are where we post devlogs/announcements and discuss topics that are better discussed with long-form writing.

## The Khonsu Labs Vision

At the core of our vision are two libraries we're developing: [BonsaiDb][bonsaidb] and [Gooey][gooey]. BonsaiDb is document database, and Gooey is a user interface framework that enables developing user interfaces for the web browser and natively through [wgpu](https://github.com/gfx-rs/wgpu).

### Why write a database engine?

The choice to develop a database in pursuit of building an MMO may seem strange. Until March 2021, [PostgreSQL](https://www.postgresql.org/) and [Redis](https://redis.io) were our intended database backends. However, as a [second contributor](https://github.com/daxpedda) joined we began to hypothesize about how to deploy a highly-available game.

Deploying highly-available PostgreSQL and Redis clusters are not easy. Our plan to minimize that stress was to have central database clusters. Yet, as we began thinking about how to build a scalable architecture, we started seeing centralized database clusters as potential bottlenecks.

For a game inspired by "single-shard" universes like [EVE Online](https://www.eveonline.com/), we wanted to be able to create a highly available database for a single "star system" in [Cosmic Verge][cosmicverge]. Trying to imagine how to manage that with PostgreSQL and Redis without drastically inflating hosting costs is what drove us to consider other options.

One day [@ecton][ecton] realized he knew enough about how [CouchDb](https://couchdb.apache.org/) worked that he could build something similar in Rust. Thus, BonsaiDb began with the initial vision being: a database built for Rust developers that supports a sqlite-style offline model, a single-server model with support for read replicas, and a quorum-based cluster model.

As we began to develop BonsaiDb's features, we started seeing the benefits of not just treating BonsaiDb as our database, but instead treating it as our application platform. We intend to have players of Cosmic Verge interacting directly with a BonsaiDb cluster that is executing the Cosmic Verge server code.

### Designing for Modularity

We strongly believe in building for re-use. As we stated earlier, we are prepared for the possibility that we can't make money building a game. We still strongly believe in the platform we're buliding it with, and we could see ourselves using [BonsaiDb][bonsaidb] and [Gooey](gooey) for other things than building [Cosmic Verge][cosmicverge].

#### User and Permissions Management

We need a robust user management system for our own needs:

- Privacy-focused: Out-of-the-box support for the needs of international privacy
  laws.
- Secure: OPAQUE key exchange for password management, client certificates,
  multi-factor authentication
- Easy-to-use: Our end-users aren't meant to be super-technical. We need to
  ensure that we've given them enough tools to not lock themselves out.
- Role-Based Access Control: Define roles and groups that can be assigned to
  users that enable functionality. The permissions system is designed with
  namespaces in mind to safely enable multiple applications running atop
  BonsaiDb.

#### Private and Group Messaging

One of the core features of an MMO is the ability to communicate with others. We believe it is also important for a social game to allow interacting with players outside of the game as well. Why should we build an in-game chat but expect everyone to use another option for out-of-game communication?

With our vision of modularity in mind, it became clear that we should be able to eat our own dogfood: Develop a standalone, self-hostable encrypted messaging platform using [BonsaiDb][bonsaidb] and [Gooey][gooey]. If done correctly, we should be able to create a reusable set of widgets that anyone could use to integrate this chat platform into their own Gooey applications as well.

The goals of the messaging platform are:

- Optional End-to-end encryption: We believe in protecting privacy. Public channels, however, don't need to be end-to-end encrypted (but they will be stored encrypted at-rest on the server).
- Moderation/Safety tools:
  - Easily report a range of chat messages to support staff.
  - Investigate feasibility/merits of parental controls/tools.
- Federation: Allow servers to deliver encrypted messages to each other. If we add microblog-like functionality, we will support [ActivityPub](https://en.wikipedia.org/wiki/ActivityPub).

#### ncog.live: A programmable multi-user virtual world

[Cosmic Verge][cosmicverge] will be our first real game (outside of ones made as kids growing up). It is good advice to try making small games before making your passion project, and we agree. Once we have a messaging platform, we want to build a programmable virtual world allows us to build the features our MMO needs but also experiment with smaller multiplayer games within this virtual world.

Our initial concept is to allow people to walk around in a virtual world, and then interact with in-world objects to launch a game. For example, sitting down at a table to play checkers. Other people could spectate the game.

The next goal would be to allow for those games to be built using WASM-based packages inside of BonsaiDb, allowing for end-users to upload their own games as well.

Once we have enough tools to build more feature-rich character-driven games with the game SDK, we will hopefully have experimented enough with game design along the way to be ready to start developing Cosmic Verge.

While we will host our own instance of this project, anyone will be able to self-host their own server as well. We are uncertain of federation capabilites at this time beyond messaging.

### Cosmic Verge

[Cosmic Verge][cosmicverge] is set in a universe where players live in an outer section of one of the arms of their galaxy. Their night sky is sometimes devoid of all nearby stars -- a near perfect black sky on some nights with the faint glow of distant galaxies.

Cosmic Verge is still early in development concept-wise. We believe in our vision of how we should eventually build Cosmic Verge, and that vision gives us plenty of time to develop the concept more completely.

[cosmicverge]: https://github.com/khonsulabs/cosmicverge
[bonsaidb]: https://github.com/khonsulabs/bonsaidb
[gooey]: https://github.com/khonsulabs/gooey
[ecton]: https://github.com/ecton