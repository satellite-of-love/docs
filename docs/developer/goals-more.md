Any [built-in goal][built-in-goals], plus any goal created with the [`goal`][apidoc-goal] function, implements [`FulfillableGoal`][apidoc-fulfillablegoal]. 

[apidoc-fulfillablegoal]: https://atomist.github.io/sdm/classes/_lib_api_goal_goalwithfulfillment_.fulfillablegoal.html (API doc for FulfillableGoal)

## GoalProjectListeners

Say you want to run tests as a separate goal. But you have to run a build
before the tests can run. By default, the goal will execute in a fresh
checkout of the repository (caveat: in [local mode][local], it may reuse a cached checkout).
Your test goal wants to run tests, it doesn't really want to run a build; it wants that to have run already.
Separately, you also want an integration-test goal and it also needs a build beforehand.

Encapsulate that "thing that needs to happen before the goal runs" in a GoalProjectListener.

### Create a GoalProjectListener

A [`GoalProjectListener`][apidoc-goalprojectlistener] function accepts a Project, 
a [`GoalInvocation`][apidoc-goalinvocation], and a GoalProjectListenerEvent ("before" or "after").
The important part is the [Project][project.md]; this is the checked-out repository that needs built 
(or whatever preparation you are encapsulating).

```typescript
async (project, inv, event) => {
        logger.error("I AM THE THING and I got event " + event);
    },
```




[`GoalProjectListenerRegistration`][apidoc-goalprojectlistenerregistration]

[apidoc-goalprojectlistener]: https://atomist.github.io/sdm/modules/_lib_api_goal_goalinvocation_.html#goalprojectlistener (API doc for GoalProjectListener)


