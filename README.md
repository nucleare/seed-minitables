# Seed Hash Table Maker

This project is an attempt to modify the proof-of-concept, found from [dsprenkels/mac-minitables](https://github.com/dsprenkels/mac-minitables)
and transform it into a theoretical SHA-256 hash table maker which pre-compute randomly generated seeds and provide a look-up table of the hashed server seeds.

Seeds are randomly generated per user upon request and once their usage is no longer needed, the unhashed form of the seed is revealed. The resulting
seed generally appears as a random hash or more accurately, a random string of numbers and letters. So in essence, the goal is to produce a lookup
table of randomly generated strings of numbers and letters and their hashed form with the aim that if you could randomly generate a seed that matches
with one of the entries on that table, you would be able to find the unhashed form of that original seed.

*Due to lack of knowledge and familiarity with the original code or how to code in general, the original names are preserved in the commands to preserve the functionality of the commands and original code themselves* _It should go without saying, this is a non-programmer's attempt at using the functionality of the original project for a different purpose_

## To Do:
[] Modify lists/popular_addrs.txt to list randomly generated strings

[] Determine functionality of the (HEX) string of that precedes each line item and adapt to text strings

[] Alternatively, manually create a list of known seed and seed hashes and save as popular_addrs.txt


## Usage [WORK IN PROGRESS - NOT PREPARED FOR USE]

```shell
# Clone the repository
git clone https://github.com/nucleare/seed-minitables.git

# Build the app
cargo build --release

# Generate the lookup-tables for a bunch of randomly generated seed strings
# THIS WILL TAKE A REALLY LONG TIME
./target/release/mac-minitables compute --table-dir tables/ lists/popular_addrs.txt 

# Add the sha256 hash of a randomly generated string of text (seed) to the file 
# designated for lookup
cat "b6237d491972f1d29ea2c0f47d4638d3cc299970f1e611149c83e25af5abe62f" > address-hash.txt

// The original git project included hashing a MAC address for lookup, therefore the following 
// command function was only adopted as part of the reverse-engineering effort and included
// merely for reference purposes.
# To confirm a known seed hash exists in the table, hash the known seed to confirm its hashed form
./target/release/mac-minitables hash 96d1a836e241f55f04d1c9ea23fbc1eca8919af844b1d76f9238c0d60628f877 | tee address-hash.txt

# Do a lookup in the tables and find a preimage of the hash
./target/release/mac-minitables lookup --table-dir tables/ "$(cat address-hash.txt)"
```

## Concept Objective
If you have a hased seed such as: <br>
`075cceb04ad1f5c62595a3f53f73e93ab12a23129c6d548bac229a5afb980e99`<br>

A lookup table would include the unhashed form:<br>
`96d1a836e241f55f04d1c9ea23fbc1eca8919af844b1d76f9238c0d60628f877`<br>

Therefore `96d1a836e241f55f04d1c9ea23fbc1eca8919af844b1d76f9238c0d60628f877` would be listed in lists/popular_addrs.txt while
`075cceb04ad1f5c62595a3f53f73e93ab12a23129c6d548bac229a5afb980e99` would be in address-hash.txt so that when you run seed-minitables
it would be able to tell you the unhashed seed was found.
