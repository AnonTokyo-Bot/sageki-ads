# sageki-ads

SaGEKI attract-mode advertisements. Each `ad_xxx.usm` is stored as its own
password-protected 7z archive split into 20 MiB parts.

- Manifest: `sageki-ads-manifest.json`
- Password: `SaGEKI@Resource`
- Primary mirror: jsDelivr
- Fallback mirror: GitHub raw content

Clients read `videos[]` and each video's `parts[]` dynamically. They download
one part at a time, publish the first completed advertisement immediately, and
then continue with later advertisements.

VP9 video chunks preserve CRI's IVF framing: the first `@SFV` payload starts
with the `DKIF` file header, and every frame retains its 12-byte IVF frame
header. Supplying raw VP9 frame payloads causes Mana decoder error
`E09031001M`.

CRI video stream chunks use a 3000-unit clock in the chunk header. For a
30 fps stream, adjacent frame timestamps advance by about 100 units while
the chunk `framerate` field remains `3000`. Writing `30` stretches a
five-minute movie to several hours from Mana's point of view and prevents
normal frame presentation.
