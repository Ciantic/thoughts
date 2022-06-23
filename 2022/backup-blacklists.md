# Backup and blacklists

This happened to one of my clients who had their site on Telia Inmics-Nebula. Virus came to the WordPress site, and during cleanup part of the media library files got deleted. No worries right, because they supposedly had daily backups?

Turns out Telia Inmics-Nebula backup strategy had blacklisted "upload" directories, and because WordPress puts the media libarary files in `wp-content/uploads` they weren't backed up.

That's basically totally useless backup. All the other files are available from the WordPress site and plugin repositories, but precisely the files user has uploaded to the site weren't backed up at all.

If you ever happen to run WordPress site on Telia Inmics-Nebula, you should be pretty worried about ransomware and viruses.
