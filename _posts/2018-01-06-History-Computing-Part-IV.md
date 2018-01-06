---
layout: post
title: "The History of Computing, Part IV: British Engineering, Polish Problem Solving, and the Wartime Glow"
---

# Hidden Communications
World War II was rife with improvements to computer technology, and much of it focused around two key areas - ballistics calculations, somewhat unsurprisingly, and cryptography. Cryptography is, simply put, the art of hiding information in plain sight - somebody wishes to send information to somebody else, without anyone but the intended recipient also being able to read it. You remember those little secret codes you came up with as kids? That's cryptography, though cryptography in the real world tends to be way more complex.

The German war effort used two cyphers, Enigma and Lorenz. Enigma was used by the military for day-to-day use, and Lorenz was used by the officers and government for important messages. Needless to say, capturing these communications was of huge importance to ending the war. Thus, a significant effort was put into breaking both cyphers.

Enigma was arguably simple. It was available commercially in the early 1920s, then developed into a more complex military version. It worked by passing letters through three sets of scrambled rotors. The first would click one position over every message, the second would move every full rotation of the first, and the third every full rotation of the second. The letter would then pass back through the rotors once more, before illuminating a bulb. These rotors could be changed for extra variance, and the military added a "plug board", allowing letters to always be swapped for one another before and after the rotors by connecting wires.

This was more complicated than any cypher seen to date. So much so, that the standard military issue Enigma used in World War II had approximately 159 quintillion different positions. Thus, breaking this by hand was rather unlikely.

# Polish Ingenuity
Poland had a keen interest in breaking Enigma, in case of another war. This effort was begun very early in the 1930s, by a team of 3 mathematicians. Marian Rejewski, a Polish mathematician, investigated the commercially available Enigma machine, and from this was able to produce a mathematical model. This was then used by Henryk Zygalski to develop a method to decrypt Enigma, known as Zygalski sheets.

Later, in what historians believe to be late 1938, Rejewski invented the "bomba kryptologiczna", or cryptologic bomb. This was a machine that could, in effect, churn through possible combinations of Enigma settings, and could extract the original settings in approximately two hours, letting operators then decode the original message. This came as the Germans began ramping up the number of encrypted messages sent. Decrypting these gave a very clear indication - they were preparing for another war.

In December 15th, 1938, the German war effort introduced two new rotors, 4 and 5, dramatically increasing the complexity of the cypher. The result of this, another very clear indication that war was afoot, was that in July 1939, Poland shared the bomba with Britain and France before it was too late. Shortly thereafter, on September 1st, 1939, Germany invaded Poland, leading Great Britain and France to declare war on Germany.

# British Developments
Located at Bletchley Park, Britain had deployed a team of mathematicians and cryptanalysts selected from among the elite, many of whom came from Oxford and Cambridge universities. The location was selected for ease of access, being roughly central to both Oxford and Cambridge, and with a rail line to London.

Among this team was the father of computing, Alan Mathison Turing, who designed the original Bombe machine in 1939, a design that was built upon by Gordon Welchman in 1940. This worked by mounting a "known plaintext" analysis - one took part of a message predicted to be in the message to decode, and attempted to find its location using known properties of the Enigma. From this, the Bombe could be used to determine the machine settings.

This allowed decryption of army and air force messages, however the German navy used 3 more wheels, hereunto unknown. Turing managed to allow parital decryption of this traffic in 1941, following the capture of a U-Boot.

# Lorenz
Lorenz was an altogether more complicated machine, relying on modulo-2 addition to encypher text, representing letters in binary using a system called the Baudot code. This proved nearly impossible to decode for the British, until August 1941, when a Lorenz operator sent a message twice, on the same machine settings, with small differences in each message. This allowed John Tiltman, another Bletchley Park mathematician, to crack the code, recovering both messages.

Tiltman passed his work on to Bill Tutte, a chemistry graduate from Cambridge University. Tutte used this to work out the structure of the machine, which was later used to create a machine, Tunny, which emulated the Lorenz. Tunny was designed and produced by Frank Morrell, and took about a month to decode each message. This was a large step up from never, but still presented a large issue, as by then the strategic importance of the message may have been lost simply due to it no longer being relevant.

# British Rube Goldbergs
Max Newman, another Bletchley analyst, worked with a team of electronic engineers to design a machine later dubbed the Heath Robinson, so named after a cartoonist who designed vastly complex machines to achieve seemingly simple tasks, much like Rube Goldberg. The Heath Robinson resembled one of these contraptions, and was hence dubbed.

The Heath Robinson automated part of the process of determining the settings of the Lorenz machine, by using various statistical techniques developed by Tutte. It used paper tape to encode both message and wheel settings, and, in a world first, did not use electromechanic components for computation. Rather, this was one of the first uses of thermionic valves (vacuum tubes) for computation. Up to this point, they were almost exclusively for radio equipment.

Valves were significantly more reliable than relays and uniselectors, having no moving parts, however suffered the problem that turning them on and off repeatedly eventually caused them to burn out, much as an incandescent lightbulb does (indeed, an incandescent lightbulb is, in fact, a thermionic valve itself, just a very simple one performing no electrical function outside of "emit light". All valves emit some level of light when turned on, and incandescent bulbs take advantage of this fact).

# A Valve Computer
Shortly thereafter, an engineer at the Post Office, Tommy Flowers, was drafted in. Flowers criticized the unreliability of the Heath Robinson, and several aspects of its design. Taking inspiration from it's valve elements, however, he went on to build a much more complex machine, capable of computing more reliably and removing electromechanical parts entirely, other than a single tape reader (actually, two, but they did the same job and were only there so one could be run while operators loaded the other).

This machine was known as Colossus. It eliminated an entire paper tape reel the Heath Robinson relied on, and did away with all relays and uniselectors, meaning significantly more reliable operation and much faster computation. This drew the criticism, as mentioned above, on valve failure upon power on, leading him to remark, "the trick is not to turn them off". Thus, the Colossus was never powered down.

By December 1943, the Mark 1 Colossus was shipped to Bletchley Park, and set up in F Block. It was operational and in January 1944, and, on February 5th, 1944, broke a German message that had not yet been cracked. Flowers was present and observed this, remarking in his journal on the day, "Colossus did its first job. Car broke down on way home." The operation of Colossus reduced the time needed to break Lorenz cyphers from weeks to mere hours, and provided crucial tactical information to British and American command centers. It was estimated that this reduced the war by 2 whole years.

The Colossus was built to be as generic as possible, meaning that as new techniques for breaking the Lorenz were found, the machine could make use of them with a minimal effort. This then lead Donald Michie and Jack Good, in February 1944, to discover a new technique to break wheel patterns quickly. Flowers was instructed, as a result of this work, to develop a new machine, the Colossus Mark 2, which had a control panel to control this particular process.

The Mark 2 was delivered to Bletchley Park on May 4th of that year, though was plagued with unreliability. It was promised to work on June 1st, however Flowers and his team were working late into the night on May 31st, diagnosing unreliability after unreliability. As midnight passed, the team retired to bed, leaving W. W. Chandler, one such engineer on the team, to work alone on the machine. The following morning, the Mark 2 was operating correctly, however a burst radiator pipe resulted in a puddle of water making its way towards the Mark 2. The navy's solution to this was for the wrens operating the machine to wear rubber soled boots while working on the machine, insulating themselves from the high voltages potentially running through the puddle.

By the end of 1944, 7 Mark 2 Colossi were in operation at Bletchley Park, dramatically aiding the D-day assault and ensuing front as the British faught to end the war. By the end of the war, 10 were in operation, with an expected delivery of an 11th shortly thereafter, which was, of course, cancelled.

# Postwar Effect
As a result of the war, Flowers was bankrupt, Newman turned down an OBE, and Turing recieved one. Prime Minister Sir Winston Churchill ordered the Colossi dismantled, and the codebreaking program was kept strictly secret despite the end of the war.

Additionally, the Government Code and Cypher School, the organisation overseeing the operation of Bletchley Park and several other codebreaking sites, became the Government Communications Headquarters, or GCHQ, which still operates today. Upon setting up and moving to Cheltenham, GCHQ took several Collosi before they were destroyed, making use of them until 1960, with one, dubbed Colossus Blue, being retired in 1959. It is not known what these were used for originally, however in the final years of their operation, they were used for training purposes.

It is known that Jack Good worked on one of these machines, on a program for the NSA, the US equivalent of the GCHQ. The program he worked on remains classified, but the NSA were prepared to commission a new machine. Implementing this on the Colossus earned Good significant prestige within the NSA, leading him to remark that "Golde told me that one of his friends who visits NSA told Golde that I am 'regarded as God' there." This demonstrates the generality built into Colossus.

# Technologies of the Time
Each of these technologies shared a commonality - they were wired for one specific job. Colossus was an outlier here, though only minorly so, in that it could be rewired to perform a different task. No, not reprogrammed, rewired. Storing "software" as data was a quirk of history that had been forgotten about, though would soon be rediscovered.

Also visible at [EsseX-Files](https://essexfiles.blogspot.co.uk/2018/01/the-history-of-computing-part-iii.html)