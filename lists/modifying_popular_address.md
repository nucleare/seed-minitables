# Explained
THe popular_addrs.txt list contains a list of 3 pairs of 2 hexadecimal digits, presumably representing the prefix of MAC addresses 
paired with their associated brand names. It is speculated that when generating the table, mac_minitables creates hashes of the
hex form and inserts the brand names as the resulting or associated outcome.

# Theoretical Changes to be made
 - Replace the column of HEX pairs with randomly generated strings
 - Replace Brand Names with a simple reference to being the unhashed seed

By replacing the popular_addrs.txt with a list of strings, it's theorized that the generated lookup table will produce a table of
strings and hashes which would be the same as mnaully taking a bunch of random strings, generating the SHA-256 hash and including
them in the table ourselves. If the structure and output of the table is as simple as we've come to conclude, then it would be 
more sensible to create a randomly list of strings using something like hashcat, using masks and rules, to generate the initial list
then appending to that list to fit the format used by the original mac_minitables.

