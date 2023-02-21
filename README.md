# StateMachine Flow

The stateMachineService are designed to guide the user through a specific sequence of steps, ensuring that each step is completed before moving on to the next. By using a state machine, the code can control the flow of the process, ensuring that the user follows the correct sequence of steps that handles the state machine for an application.

In a state machine, an event triggers a transition from one state to another. Here are some further explanations of the state transitions from the provided code: The pre-block is executed before the transition takes place, and the post-block is executed after the transition takes place.

![stateMachineFlowchart](https://user-images.githubusercontent.com/114584154/219558169-e1171a6a-71af-40f8-ab73-b02b9f451843.png)

## AppEvent
The `appEvent` is an enum that defines all the possible events that can occur within the application. Each event corresponds to a state transition in the state machine. 

AppEvent enum are:

- noSession
- authenticationCompleted
- createPasswordCompleted
- verifyTFACompleted
- tfaVerificationPending
- tfaNotVerified
- didCompleteTFA
- initialSyncCompleted
- initialSyncPending
- didCompleteInitialSync
- launchSyncCompleted
- appTourCompleted
- appTourPending
- didCompletedAppTour
- hasSession
- invalidToken
- tokenValidationCompleted
- didCompleteRefreshToken
- migration
- resync
- appMigrationCompleted
- didCompleteAppMigration
- logout

## NewAppState

`NewAppState` is a enum that represents the current state of the application. It has a single property, `currentState`, which is set to one of the values defined in the `AppStateEnum` enum.

NewAppState enum are:

- idle
- login
- verifyCreateNewPassword
- verifyTokenValidation
- refreshToken
- verifyTFA
- initiateTFA
- verifyAppMigration
- resync
- verifyAppTour
- appTour
- verifyInitialSync
- initialSync
- launchSync
- home

## State Transitions

Implementing a state machine with different states and transitions, with the goal of guiding the flow of a process. In a state machine, an event triggers a transition from one state to another. Here are some further explanations of the state transitions from the provided code:

- `idle` to `login`: This transition occurs when the `noSession` event is triggered. It moves the state from the initial `idle` state to the `login` state. It means that there is no user session, and the user must log in to continue.
- `idle` to `verifyTokenValidation`: This transition occurs when the `hasSession` event is triggered. It moves the state from the initial idle state to the `verifyTokenValidation` state. It means that there is an existing user session, and the app must verify the session token to continue.
- `login` to `verifyCreateNewPassword`: This transition occurs when the `authenticationCompleted` event is triggered. It moves the state from `login` to `verifyCreateNewPassword`. It means that the user has successfully authenticated and now needs to create a new password.
- `verifyCreateNewPassword` to `verifyTokenValidation`: This transition occurs when the `createPasswordCompleted` event is triggered. It moves the state from `verifyCreateNewPassword` to `verifyTokenValidation`. It means that the user has created a new password and now needs to validate the session token to continue.
- `verifyTokenValidation` to `verifyTFA`: This transition occurs when the `tokenValidationCompleted` event is triggered. It moves the state from `verifyTokenValidation` to `verifyTFA`. It means that the user has successfully validated the session token and now needs to verify their identity with two-factor authentication (TFA).
- `verifyTFA` to `verifyAppMigration`: This transition occurs when the `verifyTFACompleted` event is triggered. It moves the state from `verifyTFA` to `verifyAppMigration`. It means that the user has successfully verified their identity with TFA and now needs to verify the app migration.
- `verifyAppMigration` to `verifyAppTour`: This transition occurs when the `appMigrationCompleted` event is triggered. It moves the state from `verifyAppMigration` to `verifyAppTour`. It means that the app has successfully completed the migration, and the user needs to complete an app tour.
- `verifyAppTour` to `verifyInitialSync`: This transition occurs when the `appTourCompleted` event is triggered. It moves the state from `verifyAppTour` to `verifyInitialSync`. It means that the user has completed the app tour, and the app now needs to complete an initial sync.
- `verifyInitialSync` to `launchSync`: This transition occurs when the `initialSyncCompleted` event is triggered. It moves the state from `verifyInitialSync `to `launchSync`. It means that the initial sync has been completed, and the app is now ready for use.

These state transitions are designed to guide the user through a specific sequence of steps, ensuring that each step is completed before moving on to the next. By using a state machine, the code can control the flow of the process, ensuring that the user follows the correct sequence of steps.

