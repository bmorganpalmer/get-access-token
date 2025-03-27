# AWS Cognito Authentication Demo

This project demonstrates how to display an AWS Cognito access token in a web application.

## Files

1. `index.html` - Main application page with login form and token display
2. `style.css` - Styling for the application  
3. `tokenHandler.js` - Client-side JavaScript for simulating authentication and displaying the token

## How to Use

1. Place all three files in your web server directory
2. Access the application at `http://localhost:8080`
3. Enter your username and password
4. The access token will appear in a scrollable box below the form

## Implementation Notes

This demonstration uses a client-side simulation of authentication to display how token handling would work. For a production implementation, you would need to:

1. Use AWS Amplify for a fully-featured Cognito integration
2. Or implement more secure authentication using the OAuth 2.0 flow with a server-side component

## Integration with Real Cognito

To integrate with a real AWS Cognito instance:

1. Install AWS Amplify:
   ```html
   <script src="https://cdn.jsdelivr.net/npm/aws-amplify@5.0.5/dist/aws-amplify.min.js"></script>
   ```

2. Configure Amplify in your JavaScript:
   ```javascript
   const awsConfig = {
     Auth: {
       region: 'us-east-1',
       userPoolId: 'us-east-1_HBR3XpaTX',
       userPoolWebClientId: '4k39avg5kbhk68r58crojnap0e'
     }
   };
   Amplify.configure(awsConfig);
   ```

3. Replace the mock authentication in tokenHandler.js with:
   ```javascript
   async function getCognitoToken(username, password) {
     try {
       const user = await Auth.signIn(username, password);
       const token = user.signInUserSession.accessToken.jwtToken;
       return {
         success: true,
         accessToken: token
       };
     } catch (err) {
       return {
         success: false,
         error: err.message
       };
     }
   }
   ```

## Security Considerations

The current implementation is for demonstration purposes only. In a production environment:

- Never hardcode sensitive credentials in client-side code
- Use proper HTTPS for all communications
- Consider implementing token refresh mechanisms
- Store tokens securely, preferably with HttpOnly cookies
