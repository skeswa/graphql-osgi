# API concept
This is a concept for the Java API.

## Resolver
```java
@Args
interface ListArgs extends  {
  @Arg
  @Desc("Lorem ipsum")
  Boolean offset();

  @Arg
  @Desc("Lorem ipsum")
  Optional<Integer> offset();

  @Arg
  @Desc("Lorem ipsum")
  Optional<Integer> limit();
}

@Type
interface Player {
  @Field
  @Desc("Identifies a player")
  ID id();

  @Field
  @Desc("Lorem ipsum")
  Optional<String> nickName();

  @Field
  @Join("Team")
  @Desc("Lorem ipsum")
  ID currentTeam();

  @Field
  @Args(ListArgs.class)
  @Join("Team")
  @Desc("Lorem ipsum")
  Optional<List<ID>> formerTeams();
}

@Mutations
class SomeMutations {
  @Mutation
  @Desc("Lorem ipsum")
  Player createPlayer(@Arg Optional<String> nickName, @Arg("currentTeam") @Join("Team") Reference currentTeamRef, List<ID> formerTeamIds) {
    return null;
  }

  @Mutation
  @Desc("Lorem ipsum")
  Player authenticatedPlayer() {
    return null;
  }
}

interface Resolver<T> {
  List<T> resolve(Request request, List<ID> ids);
}

@Resolves("Player")
class PlayerResolver implements Resolver<Player> {
  List<Player> resolve(Request request, List<ID> ids) {
    if (req.field(Player::id).wasIncluded()) {
      req.field(Player::id).exists()
      // Add to the request.
    }

    return List.of(new PlayerImplOfSomeKind)
  }
}

```