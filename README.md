# THIS BUG HAS BEEN FIXED AS OF V1.04. THERE IS NO REASON TO USE THIS.
I am leaving this release here for archival purposes. Again: DO NOT USE THIS ANYMORE.

# The Lam Bug

It looks like the developers tried to make the Riufan Inn scene optional, but made a huge error in doing so.

The provided file here patches the recruitment event so you cannot get stuck. 

## Directions

Note: This is only usable on the PC version of the game. This is meant for the build currently active as of 4/20/2024. Steam build 14052884. Do not use this with any other build. Hopefully this bug will be fixed in the next one!

Only use this mod if you run into this bug. Set it up, recruit Lam, and then restore the file back. Do not do this if you are not comfortable editing and renaming files on your filesystem.

1. Close the game if it is running
2. Go to your game directory, and browse to: `\EiyudenChronicle_Data\StreamingAssets\aa\StandaloneWindows64`
3. Back up the file named `3a52e2d360a274202f3dab4a30b75859.bundle`. For example, rename it to `3a52e2d360a274202f3dab4a30b75859.bundle.bak`
4. Copy the `3a52e2d360a274202f3dab4a30b75859.bundle` file from here and place it in that folder.
5. Open game, complete the recruitment quest
6. Go back to `\EiyudenChronicle_Data\StreamingAssets\aa\StandaloneWindows64` and restore your back up. (For example, delete the modified file, and rename the `3a52e2d360a274202f3dab4a30b75859.bundle.bak` file back to `3a52e2d360a274202f3dab4a30b75859.bundle`.
7. Enjoy!

Note: The original file is `1,189 KB`. The mod is `10,388 KB`.

## Technical details

When you speak to Riufan, the game initializes a flag `TalkCount_ch_00580_01` and sets it to 1, indicating you talked to Riufan.

When you speak to Lam, if Riufan isn't in your party, and your `TalkCount_ch_00580_01` flag value is not set to 1, the `TalkCount_ch_00580_01` flag is incremented and saved. Theoretically, if you speak to her at some point, then come back with Riufan, you would be able to recruit her directly. However, the problem is that every time you talk to her, the `TalkCount_ch_00580_01` flag keeps incrementing, and the check to _continue_ the event is checking that `TalkCount_ch_00580_01 == 1`.

We can implement a very basic fix by changing that operation to `TalkCount_ch_00580_01 >= 1`, which is what this patch provides.
