# Summary
## API Standards
### Error Codes in Responses
#### Basic
These error codes can be returned by any API endpoint:
`M_FORBIDDEN` Forbidden access, e.g. joining a room without permission, failed login.
`M_UNKNOWN_TOKEN` The access or refresh token specified was not recognised.
An additional response parameter, `soft_logout`, might be present on the response for 401 HTTP status codes. See [the soft logout section](https://spec.matrix.org/v1.6/client-server-api/#soft-logout) for more information.
`M_MISSING_TOKEN` No access token was specified for the request.
`M_BAD_JSON` Request contained valid JSON, but it was malformed in some way, e.g. missing required keys, invalid values for keys.
`M_NOT_JSON` Request did not contain valid JSON.
`M_NOT_FOUND` No resource was found for this request.
`M_LIMIT_EXCEEDED` Too many requests have been sent in a short period of time. Wait a while then try again.
`M_UNRECOGNIZED` The server did not understand the request. This is expected to be returned with a 404 HTTP status code if the endpoint is not implemented or a 405 HTTP status code if the endpoint is implemented, but the incorrect HTTP method is used.
`M_UNKNOWN` An unknown error has occurred.
### Transaction Identifiers
After a request is finished, the `{txnId}` should be changed

## [Authentication](https://spec.matrix.org/v1.6/client-server-api/#client-authentication)
Access tokens should be provided with a request header: `Authorization: Bearer TheTokenHere`
`M_MISSING_TOKEN` or `M_UNKNOWN_TOKEN` respectively. Note that an error code of `M_UNKNOWN_TOKEN` could mean one of four things:
1.  the access token was never valid.
2.  the access token has been logged out.
3.  the access token has been [soft logged out](https://spec.matrix.org/v1.6/client-server-api/#soft-logout).
4.  **[Added in `v1.3`]** the access token [needs to be refreshed](https://spec.matrix.org/v1.6/client-server-api/#refreshing-access-tokens).
When a client receives an error code of `M_UNKNOWN_TOKEN`, it should:
-   attempt to [refresh the token](https://spec.matrix.org/v1.6/client-server-api/#refreshing-access-tokens), if it has a refresh token;
-   if [`soft_logout`](https://spec.matrix.org/v1.6/client-server-api/#soft-logout) is set to `true`, it can offer to re-log in the user, retaining any of the client’s persisted information;
-   otherwise, consider the user as having been logged out

clients indicate their support for refresh tokens by including a `refresh_token: true` property in the request body of the [`/login`](https://spec.matrix.org/v1.6/client-server-api/#post_matrixclientv3login) and [`/register`](https://spec.matrix.org/v1.6/client-server-api/#post_matrixclientv3register) 

### Registration and login
Both follow authentication flows, each containing some authentication stages. You'll have to give the right responses to the flows and their stages accordingly. If a flow is not recognized by the application, you can request an [html fallback login](https://spec.matrix.org/v1.6/client-server-api/#login-fallback)
> [!warning]
> Clients SHOULD enforce that the password provided is suitably complex. The password SHOULD include a lower-case letter, an upper-case letter, a number and a symbol and be at a minimum 8 characters in length. Servers MAY reject weak passwords with an error code `M_WEAK_PASSWORD`.

## [Capabilities](https://spec.matrix.org/v1.6/client-server-api/#capabilities-negotiation)
The capabilities describe what the homeserver can do, such as `m.set_displayname`, which has a property "enabled": false or true.
Which tells us if the server allows the users to change their name or not.

## Events
> [!warning]
> Events are ordered in this API according to the arrival time of the event on the homeserver. This can conflict with other APIs which order events based on their partial ordering in the event graph. This can result in duplicate events being received (once per distinct API called). Clients SHOULD de-duplicate events based on the event ID when this happens.

[Rich replies, threads, event replacements](https://spec.matrix.org/v1.6/client-server-api/#relationship-types)
## Rooms
Rooms are events with children such as:
- room creator
- invites
- power levels
- room name
- room topic
- memberships for users in the room
	- unrelated : cannot send or receive messaged from room
	- knocking : user has requested to join the room
	- invited
	- joined
	- banned
	- ![[Pasted image 20230304162400.png]]