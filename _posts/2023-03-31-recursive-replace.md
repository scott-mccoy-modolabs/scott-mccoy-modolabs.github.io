
# Find And Replace in Files on MacOS + zsh 

This is the best one I have found:

`find . -type f -print0 | xargs -0 perl -pi -e 's/mapspeople example/Sandbox/g'`
