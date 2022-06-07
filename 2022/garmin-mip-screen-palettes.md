# Garmin MIP screen palettes

I'm trying to develop my own watch face to Forerunner series watches which has 64 color MIP screen, same as in Fenix 7 or many other models. Garmin's webpage gives the color table:

<table class="palette" style="
    border-collapse: collapse;
">
<tbody><tr>
 <td style="background-color: #000000; color:white">&nbsp;&nbsp;</td>
 <td style="background-color: #000055; color:white">&nbsp;&nbsp;</td>
 <td style="background-color: #0000aa; color:black">&nbsp;&nbsp;</td>
 <td style="background-color: #0000ff; color:black">&nbsp;&nbsp;</td>
 <td style="background-color: #005500; color:white">&nbsp;&nbsp;</td>
 <td style="background-color: #005555; color:white">&nbsp;&nbsp;</td>
 <td style="background-color: #0055aa; color:black">&nbsp;&nbsp;</td>
 <td style="background-color: #0055ff; color:black">&nbsp;&nbsp;</td>
</tr><tr>
 <td style="background-color: #00aa00; color:black">&nbsp;&nbsp;</td>
 <td style="background-color: #00aa55; color:black">&nbsp;&nbsp;</td>
 <td style="background-color: #00aaaa; color:black">&nbsp;&nbsp;</td>
 <td style="background-color: #00aaff; color:black">&nbsp;&nbsp;</td>
 <td style="background-color: #00ff00; color:black">&nbsp;&nbsp;</td>
 <td style="background-color: #00ff55; color:black">&nbsp;&nbsp;</td>
 <td style="background-color: #00ffaa; color:black">&nbsp;&nbsp;</td>
 <td style="background-color: #00ffff; color:black">&nbsp;&nbsp;</td>
</tr><tr>
 <td style="background-color: #550000; color:white">&nbsp;&nbsp;</td>
 <td style="background-color: #550055; color:white">&nbsp;&nbsp;</td>
 <td style="background-color: #5500aa; color:black">&nbsp;&nbsp;</td>
 <td style="background-color: #5500ff; color:black">&nbsp;&nbsp;</td>
 <td style="background-color: #555500; color:white">&nbsp;&nbsp;</td>
 <td style="background-color: #555555; color:white">&nbsp;&nbsp;</td>
 <td style="background-color: #5555aa; color:black">&nbsp;&nbsp;</td>
 <td style="background-color: #5555ff; color:black">&nbsp;&nbsp;</td>
</tr><tr>
 <td style="background-color: #55aa00; color:black">&nbsp;&nbsp;</td>
 <td style="background-color: #55aa55; color:black">&nbsp;&nbsp;</td>
 <td style="background-color: #55aaaa; color:black">&nbsp;&nbsp;</td>
 <td style="background-color: #55aaff; color:black">&nbsp;&nbsp;</td>
 <td style="background-color: #55ff00; color:black">&nbsp;&nbsp;</td>
 <td style="background-color: #55ff55; color:black">&nbsp;&nbsp;</td>
 <td style="background-color: #55ffaa; color:black">&nbsp;&nbsp;</td>
 <td style="background-color: #55ffff; color:black">&nbsp;&nbsp;</td>
</tr><tr>
 <td style="background-color: #aa0000; color:black">&nbsp;&nbsp;</td>
 <td style="background-color: #aa0055; color:black">&nbsp;&nbsp;</td>
 <td style="background-color: #aa00aa; color:black">&nbsp;&nbsp;</td>
 <td style="background-color: #aa00ff; color:black">&nbsp;&nbsp;</td>
 <td style="background-color: #aa5500; color:black">&nbsp;&nbsp;</td>
 <td style="background-color: #aa5555; color:black">&nbsp;&nbsp;</td>
 <td style="background-color: #aa55aa; color:black">&nbsp;&nbsp;</td>
 <td style="background-color: #aa55ff; color:black">&nbsp;&nbsp;</td>
</tr><tr>
 <td style="background-color: #aaaa00; color:black">&nbsp;&nbsp;</td>
 <td style="background-color: #aaaa55; color:black">&nbsp;&nbsp;</td>
 <td style="background-color: #aaaaaa; color:black">&nbsp;&nbsp;</td>
 <td style="background-color: #aaaaff; color:black">&nbsp;&nbsp;</td>
 <td style="background-color: #aaff00; color:black">&nbsp;&nbsp;</td>
 <td style="background-color: #aaff55; color:black">&nbsp;&nbsp;</td>
 <td style="background-color: #aaffaa; color:black">&nbsp;&nbsp;</td>
 <td style="background-color: #aaffff; color:black">&nbsp;&nbsp;</td>
</tr><tr>
 <td style="background-color: #ff0000; color:black">&nbsp;&nbsp;</td>
 <td style="background-color: #ff0055; color:black">&nbsp;&nbsp;</td>
 <td style="background-color: #ff00aa; color:black">&nbsp;&nbsp;</td>
 <td style="background-color: #ff00ff; color:black">&nbsp;&nbsp;</td>
 <td style="background-color: #ff5500; color:black">&nbsp;&nbsp;</td>
 <td style="background-color: #ff5555; color:black">&nbsp;&nbsp;</td>
 <td style="background-color: #ff55aa; color:black">&nbsp;&nbsp;</td>
 <td style="background-color: #ff55ff; color:black">&nbsp;&nbsp;</td>
</tr><tr>
 <td style="background-color: #ffaa00; color:black">&nbsp;&nbsp;</td>
 <td style="background-color: #ffaa55; color:black">&nbsp;&nbsp;</td>
 <td style="background-color: #ffaaaa; color:black">&nbsp;&nbsp;</td>
 <td style="background-color: #ffaaff; color:black">&nbsp;&nbsp;</td>
 <td style="background-color: #ffff00; color:black">&nbsp;&nbsp;</td>
 <td style="background-color: #ffff55; color:black">&nbsp;&nbsp;</td>
 <td style="background-color: #ffffaa; color:black">&nbsp;&nbsp;</td>
 <td style="background-color: #ffffff; color:black">&nbsp;&nbsp;</td>
</tr>
</tbody></table>

I was a bit dumbfound by these palette choices, so I exported it to color table and painfully tried to use indexed mode in Photoshop. It's painful because after each operation one must flatten all layers and then choose palette to preview, it's cumbersome process to preview final image.

I asked about this from Ivan Kuckir who is the developer of excellent [Photopea](https://www.photopea.com/) and he pointed out the color scheme is RGB 4x4x4 in other words 6 bits per channel RGB. It's not some weird concoction by Garmin overlords, but sensible choice.

With that knowledge there is much easier way to preview this color scheme in Photopea, just use *Adjustment Layer* called *Posterize* with levels set to four. It doesn't have dithering but it's good enough for preview.

If one wants to take out final image with dithering, it's possible to use *Filter -> Other -> Dither* with RGB 4x4x4.