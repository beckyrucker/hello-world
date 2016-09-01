One of the most famous of the classical ciphers was the **Playfair cipher**, invented by Sir Charles Wheatstone in 1854 but popularized by Lord Lyon Playfair. The cipher was used by the British during the Boer War and World War I, and was still in use as a field-grade cipher as late as World War II, probably because it is simple to teach, fast to use, requires no special equipment, and was reasonably secure by the standards of the day; by the time enemy cryptanalysts could break the message, its contents were useless to them.

>Playfair uses a **5-square block** containing the **pass-phrase**; the letter J is mapped to I to make the 26-letter alphabet fit the 5-square block. The *pass-phrase is first filled in to the 5-square block*, then the remaining letters of the alphabet complete the 5-square block, *with duplicates removed*. For instance, the pass-phrase PLAYFAIR leads to this 5-square block:

`P L A Y F`

`I R B C D`

`E G H K M`

`N O Q S T`

`U V W X Z`

>Some variants of Playfair omit Q instead of J, or start the key from the bottom-right corner and work backwards; we’ll stick with the standard method.

The message to be encrypted is split into digrams, with J mapped to I. In addition, *no digram may use the same letter twice*, so an X is inserted if needed (some Playfair variants use Z or Q instead of X). Likewise, if the last digram has only a single letter, an X is added to the end of the message. For instance, the plain-text PROGRAMMING PRAXIS is split as:

`PR OG RA MX MI NG PR AX IS`

Then each digram is enciphered separately according to the following rules:

1. If the two letters of the digram are in the same row, they are replaced pairwise by the letters to their immediate right, wrapping around to the left of the row if needed.
2. If the two letters of the digram are in the same column, they are replaced pairwise by the letters immediately below, wrapping around to the top of the column if needed.
3. Otherwise, the first letter of the digram is replaced by the letter in the same row as the first letter of the digram and the same column as the second letter of the digram, and the second letter of the digram is replaced by the letter in the same row as the second letter of the digram and the same column as the first letter of the digram.
For instance, the PR digram is enciphered as LI, because P and R are in different rows and columns, and the OG digram is enciphered as VO, since O and G are in the same column. The complete encipherment is shown below:

`PR OG RA MX MI NG PR AX IS`

`LI VO BL KZ ED OE LI YW CN`

The coded message is thus `LIVOBLKZEDOELIYWCN`. Decryption is simply the inverse of encryption.

Playfair is rather more secure than simpler substitution ciphers because it works with digrams rather than single letters, rendering simple frequency analysis moot. Frequency analysis on digrams is possible, but requires considerably more cipher-text than frequency analysis on single letters because Playfair admits 600 digrams whereas simple substitution admits only 26 letters. Manual cryptanalysis looks at commonly-reversed digrams such as REceivER and DEcodED; if some plain-text is known (such as a standard message header), it is easy to recover at least a partial key.

The most famous use of the Playfair cipher came in 1943. David Kahn writes in The Codebreakers:

>*Perhaps the most famous cipher of 1943 involved the future president of the U.S., J. F. Kennedy, Jr. On 2 August 1943, Australian Coastwatcher Lieutenant Arthur Reginald Evans of the Royal Australian Naval Volunteer Reserve saw a pinpoint of flame on the dark waters of Blackett Strait from his jungle ridge on Kolombangara Island, one of the Solomons. He did not know that the Japanese destroyer Amagiri had rammed and sliced in half an American patrol boat PT-109, under the command of Lieutenant John F. Kennedy, United States Naval Reserve. Evans received the following message at 0930 on the morning of the 2 of August 1943:*

>`KXJEY UREBE ZWEHE WRYTU HEYFS`

>`KREHE GOYFI WTTTU OLKSY CAJPO`

>`BOTEI ZONTX BYBWT GONEY CUZWR`

>`GDSON SXBOU YWRHE BAAHY USEDQ`

>*The translation:*

>`PT BOAT ONE OWE NINE LOST IN ACTION IN BLACKETT`

>`STRAIT TWO MILES SW MERESU COVE X CREW OF TWELVE`

>`X REQUEST ANY INFORMATION.`

>*The coastwatchers regularly used the Playfair system. Evans deciphered it with the key `ROYAL NEW ZEALAND NAVY` and learned of Kennedy’s fate. […] About ten hours later, at 10:00 p.m. Kennedy and his crew was rescued.*

#Task
Your task is to write functions that encipher and decipher messages using the Playfair cipher. 
