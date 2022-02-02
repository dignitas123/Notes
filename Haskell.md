https://testnets.cardano.org/en/programming-languages/plutus/resources/ (cardano testnet docs)
https://learnxinyminutes.com/docs/haskell/
https://replit.com/languages/haskell
https://github.com/proyecto26/cardano-developer/blob/main/CODE_HASKELL.md

install with brew
brew cask install haskell-platform
brew install haskell-stack

Invoke interpreter
stack ghci

install newest version
download https://www.haskell.org/ghc/download_ghc_9_0_2.html#macosx_x86_64
// still have issues with Xcode so I have version 8.10.7

start a script in folder
stack script helloworld.hs --resolver lts-14.18 // (also installs ghci)
or
ghci
:load helloworld.hs
:script helloworld.hs

Start project template
stack new myproject simple

build
stack build

run
stack exec myproject

test
stack test
