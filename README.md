# FPEFF1

> 💡 This repository is no longer actively maintained by DB Systel GmbH. Its development will continue here: https://github.com/xformerfhs/FPEFF1

Visual Basic .Net class for the format preserving encryption algorithm FF1 as specified in [NIST Special Publication 800-38G (February 2019)](https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-38Gr1-draft.pdf "NIST SP 800-38Gr1").

## Format Preserving Encryption
[Format preserving encryption](https://en.wikipedia.org/wiki/Format-preserving_encryption "FPE") is an cryptographic method to encrypt and decrypt data in such a way that the encrypted data is in the same format as the original data. I.e. if the original data are 16-digit credit card numbers then the encrypted data are 16-digit data, as well. This way one can encrypt data even for systems that do not know how to handle encrypted data.

This form of encryption is not restricted to numbers. One could also use texts. However, before the encryption a mapping from the letters to the numbers has to be done. After the encryption there has to be a mapping from the numbers back to the letters. Here is an example that maps the characters to numbers:

      <=> 0 Note: This means, blank is mapped to 0
    A <=> 1
    B <=> 2
    ...
    Z <=> 26

If one has the text "HOWDY THERE HOW ARE YOU" it would first be converted to the following numbers:

    8,15,23,4,25,0,20,8,5,18,5,0,8,15,23,0,1,18,5,0,25,15,21

This is then encrypted with a certain key and a certain tweak to

    21,14,10,3,20,20,8,14,20,18,13,1,3,24,2,2,2,22,6,20,3,22,24

which is then mapped to the text "UNJCTTHNTRMACXBBBVFTCVX".

## Usage
This project contains a shared class "FF1" that implements the algorithm mentioned above. Additionally it contains a simple command line program to interface to the FF1 class. There are also various unit tests included.

The command line program can be used like this:

    fpeff1 encrypt 10 0,1,2,3,4,5,6,7,8,9 2B7E151628AED2A6ABF7158809CF4F3C 39383736353433323130

This means: Encrypt the base 10 numbers "0,1,2,3,4,5,6,7,8,9" with the FF1 algorithm using the key "2B7E151628AED2A6ABF7158809CF4F3C" and the tweak "39383736353433323130". The expected output is:

    6,1,2,4,2,0,0,7,7,3

The decryption would be

    fpeff1 decrypt 10 6,1,2,4,2,0,0,7,7,3 2B7E151628AED2A6ABF7158809CF4F3C 39383736353433323130

which should yield

    0,1,2,3,4,5,6,7,8,9

## Caveat
According to [this article](https://link.springer.com/chapter/10.1007%2F978-3-319-96884-1_8 "The Curse of Small Domains") the length of the data must be at least 6 numbers, i.e. the domain size has to be at least one million elements.

## Contributing
Feel free to submit a pull request with new features, improvements on tests or documentation and bug fixes.

## Contact
Frank Schwab ([Mail](mailto:frank.schwab@deutschebahn.com "Mail"))

## License
FPEFF1 is released under the Apache V2 license. See "LICENSE" for details.
