+++
title="API - Kraken"
weight = 9
+++

# Twitch API - Kraken (Deprecated, removal not scheduled)

To make an application that uses the Twitch API, you first need to register your application on the Twitch developer site. When creating this app, enter your redirect URI, which is where your users are redirected after being authorized.

Once you create a developer application, you are assigned a client ID. Some authentication flows also require a client secret, which you can generate on the same page as the client ID.

* Client IDs are public and can be shared (for example, embedded in the source of a Web page).
* Client secrets are equivalent to a password for your application and must be kept confidential. Never expose it to users, even in an obscured form.

Because your client secret is confidential, we cannot show it to you once you leave the page, so make sure to record it somewhere safe. Also, generating a new client secret immediately invalidates the current one, which might make your API requests fail until your app is updated.

Warning: Client IDs should be unique for each application: do not re-use client IDs across multiple applications. Also, applications should request the appropriate set of scopes for the intended target APIs. Failure to adhere to these guidelines may result in the suspension of your application’s access to the Twitch API.

You can create new application on the [Twitch Developer Console](https://glass.twitch.tv/console/apps/create)

## As Module: Twitch4J

To use Helix you need to enable the Helix API when building the Twitch4J Instance, as shown below:

```java
TwitchClient twitchClient = TwitchClientBuilder.builder()
    ...
    .withEnableKraken(true)
    ...
    .build();
```

## Standalone

Initialize the Helix API as Standalone Module:

```java
TwitchKraken client = TwitchKrakenBuilder.builder()
    .withClientId("clientId")
    .withClientSecret("clientSecret")
    .build();
```

## Consume the Results

This API Client provides you 3 methods to consume the results.

### Synchronous Execution

You can execute any api call synchronously with the execute() method, as shown in the following example:

```java
UserList userList = twitchClient.getHelix().getUsers(null, null, Arrays.asList("twitch4j")).execute();
```

### Asynchronous Execution

You can execute any api call asynchronously with the queue() method, as shown in the following example:

```java
Future<UserList> userListCall = twitchClient.getHelix().getUsers(null, null, Arrays.asList("twitch4j")).queue();
```

You can retrieve the result of the command by using the Future:

```java
UserList userList = userListCall.get();
```

### Reactive Execution

You can also observe the results of any api call as an Observable by using one of the following methods:

* observe() — returns a “hot” Observable that executes the command immediately, though because the Observable is filtered through a ReplaySubject you are not in danger of losing any items that it emits before you have a chance to subscribe
* toObservable() — returns a “cold” Observable that won’t execute the command and begin emitting its results until you subscribe to the Observable

```java
Observable<UserList> userListObservable = twitchClient.getKraken().getUsers(null, null, Arrays.asList("twitch4j")).observe();
```

You then retrieve the value of the command by subscribing to the Observable:

```java
userListObservable.subscribe(data -> {
    // your code to work with the result data
});
```

## API Methods

All methods that were added to helix have been removed from the kraken module, please use those instead.

ChannelFeed:
- Open for Contributions

Chat:
- Open for Contributions

Collections:
- Open for Contributions

Ingests:
- [Ingests -> Get All](./ingests-get)

Teams:
- [Teams -> Get All](./teams-all)
- [Teams -> Get by Name](./teams-by-name)