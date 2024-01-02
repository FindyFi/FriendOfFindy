---
page_type: sample
languages:
- node.js
- sh
description: "A code sample demonstrating issuance and verification of verifiable credentials."
urlFragment: "FriendsOfFindy"
---
# Verified ID idTokenHint Sample for node.js

This code sample demonstrates how to use Microsoft Entra Verified ID to issue and consume verifiable credentials.

## About this sample

Welcome to Microsoft Entra Verified ID. In this sample, we'll teach you to issue your first verifiable credential: a Verified Credential Expert Card. You'll then use this card to prove to a verifier that you are a Verified Credential Expert, mastered in the art of digital credentialing. The sample uses the preview REST API which supports ID Token hints to pass a payload for the verifiable credential.

## Deploy to Azure

Complete the [setup](#Setup) before deploying to Azure so that you have all the required parameters.


[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FFindyFi%2FFriendsOfFindy%2Fmain%2FARMTemplate%2Ftemplate.json)

You will be asked to enter some parameters during deployment about your app registration and your Verified ID details. You will find these values in the admin portal.

## Additional appsettings that can be used after deployment

These settings can be set in the deployed AppServices Environment Variables configuration. 

| Key | value | Description |
|------|--------|--------|
| issuancePinCodeLength | 0-6 | Length of pin code. A value of 0 means not to use pin code during issuance. Pin code is only supported for [idTokenHint flow](https://learn.microsoft.com/en-us/entra/verified-id/how-to-use-quickstart). If the webapp is used on a mobile device, the sample eliminates the pin code as it makes no sense. |
| useFaceCheck | true/false | If to use FaceCheck during presentation requests. This requires that the credential type asked for has a photo claim. |
| photoClaimName | claim name | The name of the claim in the credential type asked for during presentation when `useFaceCheck` is `true`. The PhotoClaimName is not used during issuance. If the credential manifest has a claim with a type of `image/jpg;base64url`, that claim will hold the photo. You can override the name of the photo claim by specifying it as a query string parameter, like `/verifier?photoClaimName=photo`. |
| matchConfidenceThreshold | 50-100 | Optional. Confidence threshold for a successful FaceCheck. Default is 70 |

## Test Issuance and Verification

Once you have deployed this sample to Azure AppServices with a working configuration, you can issue yourself a `Friends of Findy` credential and then test verification. 

*Note - FaceCheck is in preview. If you plan to test it, make sure you have the latest Microsoft Authenticator.

## Setup

Before you can use Verified ID you need to onboard to it. You can either onboard using the [quick setup](https://learn.microsoft.com/en-us/entra/verified-id/verifiable-credentials-configure-tenant-quick) method or the [manual setup](https://learn.microsoft.com/en-us/entra/verified-id/verifiable-credentials-configure-tenant) method. In the manual method, you use your own Azure Key Vault to store your signing key.

### Create application registration
Follow the documentation for how to do [app registeration](https://learn.microsoft.com/en-us/entra/verified-id/verifiable-credentials-configure-issuer#configure-the-verifiable-credentials-app) for an app with permission to Verified ID.

## Setting up and running the sample
To run the sample, clone the repository, compile & run it. It's callback endpoint must be publically reachable, and for that reason, use a tool like `ngrok` as a reverse proxy to reach your app if you're running it on `localhost`.

```sh
git clone https://github.com/FindyFi/FriendsOfFindy.git
cd FriendsOfFindy/node-app
npm install
npm run
```

### Create your credential
To use the sample we need a configured Verifiable Credential in the azure portal.
In the project directory [CredentialFiles](../CredentialFiles) you will find the [VerifiedCredentialExpertDisplay.json](../CredentialFiles/VerifiedCredentialExpertDisplay.json) file and the [VerifiedCredentialExpertRules.json](../CredentialFiles/VerifiedCredentialExpertRules.json) file. Use these 2 files to create your own VerifiedCredentialExpert credential.

If you navigate to your [Verifiable Credentials](https://portal.azure.com/#blade/Microsoft_AAD_DecentralizedIdentity/InitialMenuBlade/issuerSettingsBlade) blade in azure portal, follow the instructions how to create your first verifiable credential.

You can find the instructions on how to create a Verifiable Credential in the azure portal [here](https://aka.ms/didfordev)

## Receiving a credential
1. Open [friends.findy.fi](https://friends.findy.fi/) in your browser.
2. Select `Issue Credential`
3. In Authenticator, scan the QR code. 
> If this is the first time you are using Verifiable Credentials the Credentials page with the Scan QR button is hidden. You can use the `Add account` button. Select `other` and scan the QR code, this will enable the preview of Verifiable Credentials in Authenticator.
4. Select **Add**.

## Verifying the verifiable credential
1. Navigate back (or re-open [friends.findy.fi](https://friends.findy.fi/)) in your browser and select `Verify Credential`
2. Check the `Use FaceCheck` checkbox and click the `Verify Credential` button
3. Scan the QR code and choose `Next`
4. Scan your face with the camera
4. Select `Share`
5. You should see the result presented in the browser.

## More information

For more information, see MSAL.NET's conceptual documentation:

- [Quickstart: Register an application with the Microsoft identity platform](https://docs.microsoft.com/azure/active-directory/develop/quickstart-register-app)
- [Quickstart: Configure a client application to access web APIs](https://docs.microsoft.com/azure/active-directory/develop/quickstart-configure-app-access-web-apis)
- [Acquiring a token for an application with client credential flows](https://aka.ms/msal-net-client-credentials)
