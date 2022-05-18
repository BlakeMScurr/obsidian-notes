 - Web 2 applications are largely data constrained
 - DA is not really solved
 - Defi is a mess of scams because there are few fundamentals
 - We can create neutral but non robust centralised services with ZKPs and slashing for DA



How does it work?

We have one party called the steward who holds all the data. They have a bond and gradually earn money from it. People buy space on their servers. You buy space in uint256 sized chunks. You might buy 100,000 for a given price. That money goes into their bond. When you store data, you just send the data and receive a receipt saying it will go into the store at a particular time. If they're non responsive, you put it into the queue, which they must respond to or their bond is slashed. To get on the queue you must show that this is your nth message less than the total allowance, and you lose the right to post if the steward can demonstrate a message greater than n, or one at n with a different value, this limits you to your allowance. At given intervals, the steward posts a hash of all data on chain, and a proof that all data in the previous lot is in this lot, and that it's properly ordered. Anyone can request message i for user x, and such a message can, again be put on the on chain queue. Stewardship can be sold to another party.

Steward
Bond
Post
Get
Queue
Snapshot
Lease
Transfer


Crypto has solved money. It's trivial to create a token that works as money: it won't disappear on you, it won't be sent to anyone else, it won't be inflated. Wars are fought over the control of money, and exercising that control harms the real economy.

Messaging, Social Networks, Marketplaces, Codebases, Encyclopedias.


_________

The people who controlled the money used to wield inescapable power over us. The battle for control over the money supply sucked in generations of bright economists. Wielding that power has always benefited the powerful at the expensive of everyone else. Cryptocurrency is money that can't be controlled. It operates according to specified rules, and while the people involved might seek their own advantage at every turn, the system as a whole is credibly neutral.

In the early 2000s, founders following utopian visions and profits inadvertently created new and unprecedented centres of power. Google's founding mission was "to organize the world's information and make it universally accessible and useful." YouTube's was "to give everyone a voice and show them the world." Twitter's "to give everyone the power to create and share ideas and information instantly without barriers." Now each of these companies mediates the world's information, huge battles are fought over the way they moderate, and the world is impoverished for their intervention.

Ethereum was supposed to bring the triumph of Bitcoin from money into the world at large, and it seems perfectly suited to build neutral institutions to replace tech giants. Unfortunately, Ethereum is limited to processing a tiny amount of data and computation every 10 seconds in a little block. Sharding and rollups will improve computation and data throughput immensely, but even close to enough to run a system like Google Search.

To make our new centres of power credibly neutral, we have to think of Ethereum as a court. We simply use our search engine as normal, but we keep the receipts, and hold it accountable on Ethereum if it acted poorly. 