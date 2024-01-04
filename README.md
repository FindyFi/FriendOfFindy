# Friend of Findy sample

This repo contains a sample Microsoft Entra Verified ID application. The application is running at [friend.findy.fi](https://friend.findy.fi)

It is forked from https://github.com/Azure-Samples/active-directory-verifiable-credentials-node and modified to enable issuing and verifying of "Friend Credentials".

## Setup

1. To set up your Entra Verified ID environment, you can follow the setup instructions [here](https://aka.ms/vcsetup).
2. [Register a new app](https://learn.microsoft.com/en-us/entra/verified-id/verifiable-credentials-configure-tenant#register-an-application-in-azure-ad) in the Microsoft identity platform and [generate an application secret](https://learn.microsoft.com/en-us/entra/verified-id/verifiable-credentials-configure-issuer#configure-the-verifiable-credentials-app). Set the values for `ClientId` and `ClientSecret` in the [config.json](node-app/config.json) file.
3. Modify [FriendOfFindyDisplay.json](CredentialFiles/FriendOfFindyDisplay.json) and [FriendOfFindyRules.json](CredentialFiles/FriendOfFindyRules.json) to set up your own friend credential format. See [documentation](https://learn.microsoft.com/en-us/entra/verified-id/rules-and-display-definitions-model).
4. Go to [Credentials](https://entra.microsoft.com/#view/Microsoft_AAD_DecentralizedIdentity/CardsListBlade) section in Microsoft Entra admin center and add a new credential. Copy and paste the contents of JSON files above to `Display definition` and `Rules definition` fields. Go to the `Issue credential` section and copy the `authority`, `type`, and `manifest` values to [node-app/config.json]'s fields `DidAuthority`, `CredentialType` and `CredentialManifest`. Copy the value of `DidAuthority` also to `acceptedIssuers`.
5. [Run the Node application](node-app#setting-up-and-running-the-sample) locally and see that it at least starts. Use [ngrok](https://ngrok.com/) if you want to test issuing and verifying (API callback's don't work with `localhost` URLs).
5. [![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FFindyFi%2FFriendOfFindy%2Fmain%2FARMTemplate%2Ftemplate.json) - you need to fill in values from your [config.json](node-app/config.json) file.


 
