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
