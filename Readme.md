#Standard Galactic Time
This proposal is currently in version 1. If you have any suggestions, 
feel free to post up an issue, or file a pull request, and your 
changes can be discussed
##Table of contents
* The Basic Idea
* Timestamps and use in code
* Use in formal writing and speech
* Use in informal writing and speech
* Other Ideas

##The Basic Idea
The reasoning for this can be found [here](http://www.reddit.com/r/0x10c/comments/14996o/time_in_the_0x10c_universe/).
As a summary, our time system is fairly confusing, what with different 
gradations for each value. Not to mention that all of the values are 
based on Earth's rotations and revolutions, and in the age of 0x10c, 
Earth likely no longer exists.

It was with this discussion that a base ten system be developed. At 
the most basic level, the current 'stardate' is just a decimal 
representation of seconds starting at what I will call the 0x10c 
epoch. This starts at January 1, 1988 (the year our traveller's were 
lost). We are using seconds, and not ticks, so as to maintain 
understanding, when clock specifications call a second 60 'ticks'.

Since using this number, which as of the beginning of 2013 was over 
.75 billion, would quickly become unweildy naming terms and 
gradations were devised for an easy conveyance of time. The table 
below will show how seconds are divided, and their equivalent Earth 
Periods.
<table>
<tr><td>Number of seconds</td><td>Power of Ten</td><td>Earth Period</td></tr>
<tr><td>1</td><td>10<sup>0</sup></td><td>1 second</td></tr>
<tr><td>1,000</td><td>10<sup>3</sup></td><td>About 17 Minutes</td></tr>
<tr><td>100,000</td><td>10<sup>5</sup></td><td>About 1 Day</td></tr>
<tr><td>10,000,000</td><td>10<sup>7</sup></td><td>About 1 Season (quarter year)</td></tr>
<tr><td>1,000,000,000</td><td>10<sup>9</sup></td><td>About 33 years</td></tr>
</table>

Each of these divisions is separated by a period (.) thus, a rough 
calculation (not taking into account leap seconds/days) of Midnight, 
January 1, 2013 would be 78.84.00.000.  More use of this will be 
covered below.

##Timestamps and use in code
In this section, I would like to layout an easy standard timestamp 
that will be able to convey dates both in our era, and the years 
following the wakeup.

###Size
To start with, I propose a 32bit timestamp. This is small enough 
that no program/protocol/OS/CS should have any problem storing it. 
It is large enough though, that unsigned, it will give us atleast 136 
years of use (which I propose will end up being shorter. 32bit math 
is also much simpler than 48 or 64, and will prevent storing words 
full of unset bits.

###Handling Two Eras
It has been stated (though not in stone) that communication will be 
possible between the DCPU and the real world via the 'Hyperverse'. 
In order to differentiate between eras, I propose setting the most 
significant bit to 0 for current era, and 1 for future era. It is also 
possible to sign the timestamp, and make the current era 'negative'. 
I propose against this, as counting forward in time by subtracting 
seconds is counterintuitive.