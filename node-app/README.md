# Friend of Findy verifiable credential Node.js app

This code sample demonstrates how to use Microsoft Entra Verified ID to issue, present, and verify verifiable credentials.

Once you have deployed this sample to Azure AppServices with a working configuration, you can issue yourself a `Friends of Findy` credential and then test verification. 

*Note - FaceCheck is in preview. If you plan to test it, make sure you have the latest Microsoft Authenticator.

### Create application registration
Follow the documentation for how to do [app registration](https://learn.microsoft.com/en-us/entra/verified-id/verifiable-credentials-configure-issuer#configure-the-verifiable-credentials-app) for an app with permission to Verified ID.

## Setting up and running the sample
To run the sample, clone the repository, compile & run it. It's callback endpoint must be publically reachable, and for that reason, use a tool like `ngrok` as a reverse proxy to reach your app if you're running it on `localhost`.

```sh
git clone https://github.com/FindyFi/FriendOfFindy.git
cd FriendOfFindy/node-app
npm install
npm run
```

## Receiving a credential
1. Open the app in your browser. (Our version can be found at [friend.findy.fi](https://friend.findy.fi/).)
2. Select `Get credential`
3. Send a photo of yourself or take a selfie. Click `Issue Credential`.
3. In Authenticator, scan the QR code and submit the attached PIN code.
> If this is the first time you are using Verifiable Credentials the Credentials page with the Scan QR button is hidden. You can use the `Add account` button. Select `other` and scan the QR code, this will enable the preview of Verifiable Credentials in Authenticator.
4. Select `Add`.

## Verifying the verifiable credential
1. Navigate back to the main page (or re-open [friend.findy.fi](https://friend.findy.fi/)) in your browser and select `Show credential`
2. Check the `Use FaceCheck` checkbox and click the `Verify Credential` button
3. Scan the QR code and choose `Next`
4. Scan your face with the camera
4. Select `Share`
5. You should see the result presented in the browser.

## Additional appsettings that can be used after deployment

These settings can be set in the deployed AppServices Environment Variables configuration. 

| Key | value | Description |
|------|--------|--------|
| issuancePinCodeLength | 0-6 | Length of pin code. A value of 0 means not to use pin code during issuance. Pin code is only supported for [idTokenHint flow](https://learn.microsoft.com/en-us/entra/verified-id/how-to-use-quickstart). If the webapp is used on a mobile device, the sample eliminates the pin code as it makes no sense. |
| useFaceCheck | true/false | If to use FaceCheck during presentation requests. This requires that the credential type asked for has a photo claim. |
| photoClaimName | claim name | The name of the claim in the credential type asked for during presentation when `useFaceCheck` is `true`. The PhotoClaimName is not used during issuance. If the credential manifest has a claim with a type of `image/jpg;base64`, that claim will hold the photo. You can override the name of the photo claim by specifying it as a query string parameter, like `/verifier?photoClaimName=photo`. |
| matchConfidenceThreshold | 50-100 | Optional. Confidence threshold for a successful FaceCheck. Default is 70 |

## About this sample

This repo is forked from https://github.com/Azure-Samples/active-directory-verifiable-credentials-node and modified to enable issuing and verifying of "Friend Credentials".
