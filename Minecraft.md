# Using CraftStudio for modding Minecraft #

CraftStudio's 3D box-based models are compatible with Minecraft. You can get CraftStudio to generate a `Model_____.java` file that can be used with the [Minecraft Coder Pack](http://mcp.ocean-labs.de/) using the `/export minecraft` chat command in the model editor.

Some things to note:

 * Animations are not supported, because as of 1.8, Minecraft doesn't have support for key-framed animations, only simple hard-coded ones.
 * You should only use the "Full" unwrap mode for your texture. Other modes are not supported in the exporter.
 * You can use `/export texture` to export your PNG too.

Various teams like [Elkyos](http://pinterest.com/elkyos/elkyos/) or [SimCraft](http://www.simcraft.co.za/) have used CraftStudio successfully to make 3D models for their servers.

Fun example: Replacing the Minecraft pig by a huge AT-AT model:

![xjSDl.png](https://bitbucket.org/repo/ey9q4X/images/1240169626-xjSDl.png)

## Alternative export format ##

If your modding team is willing to go much deeper, you can use `/export json model` and `/export json animation` to export models and animations in a simple custom JSON format. You can then convert those files into your own format and/or build the required runtime classes to play back animations.

That would probably involve adding a Quaternion math class to Minecraft to interpolate rotation keyframes properly and basically making many changes in Minecraft's model rendering code. Tthe JSON format stores Euler angles to be applied in YXZ order (aka. yaw / pitch / roll).