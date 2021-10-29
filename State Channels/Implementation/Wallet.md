#flashcards
# Browser Wallet

What complexities does the channel client API handle for us?
?
Key management
Ethereum providers
Nitro internals


What do we need to import to use the channel client API?
?
@statechannels/channel-client
@statechannels/iframe-channel-provider

What does @statechannels/channel-client do?
?
It exposes a friendly API for the Dapp
<!--SR:2021-10-29,1,230-->

What does @statechannels/iframe-channel-provider do?
?
It is the lower level
<!--SR:2021-10-29,1,230--> 

How do you enable the channel provider?
?
// Attaches the channel provider to the window object
require('@statechannels/iframe-channel-provider');
await window.channelProvider.mountWalletComponent('https://xstate-wallet-v-0-3-0.statechannels.org');
await window.channelProvider.enable();

When should one call `window.channelProvider.enable();`?
?
When the user presses some kind of "connect with MetaMask" button, so that the MetaMask prompt isn't jsut aggressively thrust on the user.
<!--SR:2021-10-29,1,230-->

How does having the wallet served as an iFrame improve security?
?
The app can't read the wallet's code or storage.
The wallet can associate policies like whitelists to various domains.
<!--SR:2021-10-29,1,230-->

When will the state channels wallet prompt (and not prompt) the user for explicit approval?
?
The user is prompted when `.enable()` is called.
The user is not prompted for every state update, as those could happen many times a second.
<!--SR:2021-10-29,1,230-->

What key does the state channels wallet use to sign states?
?
It creates an "ephemeral key" to sign states silently, rather than using the Ethereum key.
<!--SR:2021-10-29,1,230-->

What is a domain budget?
?
A domain budget sets the max send and receive amount for a specific asset type. This means channels can silently be opened and closed as long as the amounts remain within the budget.
<!--SR:2021-10-29,1,230-->