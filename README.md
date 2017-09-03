# midtskog.github.io
All in one IOTA paper wallet generator, capable of running offline.

The service is hosted here: https://midtskog.github.io/
If you want the application to run offline, then simply click the "offline generator" in the top right corner which will download a single html file with all scripts, css and graphics baked into it. The application can run completely without internet connection as there are no server-client requests/responses going on.
A precursor for using this is that you have installed a modern HTML5 capable web-browser, preferably the latest versions of Chrome or Safari. I have tested it in Microsoft Edge as well, and it seems to render it just fine there. If you are an IE user, I offer no guarantees that you will experience the application the way I designed it.
Dependencies inside the project are:
- QRius (qrious.min.js 4.0.2)
- IOTA lib (latest iota.min.js)
- JQuery (jquery-3.2.1.min.js).
How to use it:
A paper wallet is a way of "remembering" a specific seed and or address which can be used for receiving values or non-value transactions. So if you are vary of storing this information digitally (in a text file, in the cloud etc), a paper wallet could store this for you "off-the-grid". Then of course, you would have to physically store the paper wallet somewhere safe, and perhaps have two copies of the same paper wallet stored at two different locations to minimize the chance of information destruction.
STEP 1, pick design:
Here you choose what kind of information the paper wallet should contain.
[SEED STORE] will contain the seed as QR and plain text in a 9 by 9 matrix (read from left to right downwards).
[ONLY QR] will contain two QRs, one for the seed and one for the first address derived from the seed.
[DETAILED] will contain same two QRs from [ONLY QR] in addition to having both seed and address as plain text.
Green, cyan, violet...etc are the colors you can pick for the paper wallet. Pick the one you find most appealing!
STEP 2, seed method:
Now, you choose how the seed should be provided. If you want to type all the 81 characters (trytes) yourself, or if you have generated a seed with eg. KeePass, then use the manual option.
If you think that you are bad at pressing random keys on your keyboard, then use the crypto/entropy option. If you pick this one - you simply click "SET TRYTE" 81 times. For each cell it will generate random chars (A-Z + 9) about 100 times each second (with javascript.crypto), and the user is "deciding" which last random tryte will be set upon interaction (SET TRYTE).
Optionally you can click auto-generate, which will reset the matrix and do the user interaction for you. You can also combine auto-generate and set tryte, so the tryte determination is both artificial and organic.
In my opinion, clicking SET TRYTE 81 times gives the highest level of entropy, especially if you randomize when you decide to click (eg. click 20 times...go make yourself some coffee...click 30 more times...wash the dishes...and so on :P).
STEP 3, input/create seed:
Based on the option you picked in STEP 2, you will either see a text input field or a 9 by 9 matrix for creating your seed. It is all self explanatory when you see it.
STEP 4, derive address:
As of now, I have disabled user interaction at this step. So depending on the seed you ultimately ended up with, one public (receive) address will be generated using key index 0 and security option 2 (162-trit security). I experienced that using a key index higher than 0 for completely new seeds could screw up receiving values. This is because the paper wallet works on the outside of the tangle (necessary for generating paper wallets offline), and is therefore non-deterministic (regarding the tangle). On the light wallet for example, the key index will stop to increment once it finds the first address without a tx...and for new seeds, this will always be key index 0. So deriving an address from your completely new seed with a key index = 5 for example, then you would need to do 5 deterministic txs with the seed before you can see the value sent to the non-deterministic address you created with key index 5, and that is inconvenient for the end user. Setting different security settings is also inconvenient for the end user, as you would need to for example alter the json config data of the light wallet in order to receive values on addresses that are generated with 81 or 243 trit security.
So for now, no user interaction at step 4. Will see what I do about that in the future.
STEP 5, print/save:
All is done, and the paper wallet can be printed. You can select if you want 1, 2 or 3 copies of the paper wallet on the printing page. Or you could save the paper wallet as an image and print/use it somewhere else.
ONCE THE PAPER WALLET IS GENERATED:
You can now send values to the address generated, BE VERY CAREFUL AND DO NOT SEND VALUES TO THE SEED, sending values to a seed is exactly the same as sending values to a public address which you dont have the private key for!
SEEDS are 81 in length, ADDRESSES are 90 in length (well...with checksums).
QR:
The seed is printed with ECC option "H", which means that the QR is more robust and will validate even if it gets dirty and some parts of it becomes unreadable.
The address is printed with ECC option "Q", which is slightly less tolerant of unreadable parts - but still quite robust.
More info here: http://www.qrcode.com/en/about/error_correction.html
This is the initial release, so the service might get some modifications in the future - all depending on the feedback I receive.
Happy printing!
