# HypotheticalRBAC

## Task
- Email registration flow for basic users
- Login for both user types (basic/admin)
- Reset password via email flow for both user types
- Admin page that lists all users (protected route)

## Suggested implementation
- JWT authorization in .NET. We can write a custom Authorize attribute that can be added to the controller action methods that require authorization and/or a specific role.
- Email confirmation will include a link with a JWT as a query parameter. This JWT was created with the user's email address as a payload, and the link goes to a verification endpoint on the server that can validate the JWT.
- Password reset can be handled similarly on a separate endpoint. The link will be to a reset page and will include the JWT created with the user's email address as a query param. If it does not verify, reroute to an error page; otherwise, allow the user to reset their password.
- The base logic for JWT creation and verification is in Microsoft.IdentityModel.Tokens and System.IdentityModel.Tokens.Jwt.

## Questions to resolve
- Email server details. Are we using outgoing emails anywhere else in the application, or just for new registrations and password resets?
- Password requirements
- How should new admin users be registered? Okay to just do manually through the API or does there need to be a UI for this?
- Postman team or shared collections? Or other API test application?
- Other admin actions aside from listing users?
- How are secrets handled in our codebase? Environment variables, find/replace based on a vault, just commit it, etc.
