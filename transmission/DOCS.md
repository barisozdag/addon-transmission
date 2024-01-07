# barisozdag's Personal Home Assistant Add-ons: Transmission

Small and powerful Torrent client for Home Assistant with custom UI.

## Installation

The installation of this add-on is pretty straightforward and not different in
comparison to installing any other Home Assistant add-on.

1. [![Add repository to your Home Assitant instance.][repository-badge]][repository]
1. Click the Home Assistant My button below to open the add-on on your Home
   Assistant instance.

   [![Open this add-on in your Home Assistant instance.][addon-badge]][addon]

1. Save the add-on configuration.
1. Start the "Transmission" add-on.
1. Check the logs of the "Transmission" to see if everything went well.
1. Login to the web interface.

## Web-UI

You can access web-ui with ingress function. If you set PORT, Web-UI can be
found at `<your-ip>:9091`.

## Configuration

**Note**: _Remember to restart the add-on when the configuration is changed._

Example add-on configuration:

```yaml
log_level: info
authentication_required: false
username: ""
password: ""
download_dir: /media/downloads
incomplete_dir: /media/downloads/incomplete
uitheme: default
```

**Note**: _This is just an example, don't copy and paste it! Create your own!_

### Option: `log_level`

The `log_level` option controls the level of log output by the addon and can
be changed to be more or less verbose, which might be useful when you are
dealing with an unknown issue. Possible values are:

- `trace`: Show every detail, like all called internal functions.
- `debug`: Shows detailed debug information.
- `info`: Normal (usually) interesting events.
- `warning`: Exceptional occurrences that are not errors.
- `error`: Runtime errors that do not require immediate action.
- `fatal`: Something went terribly wrong. Add-on becomes unusable.

Please note that each level automatically includes log messages from a
more severe level, e.g., `debug` also shows `info` messages. By default,
the `log_level` is set to `info`, which is the recommended setting unless
you are troubleshooting.

### Option: `authentication_required`

This option can be used to password protect the web-ui.

### Option: `username`

The username for authentication.

### Option: `password`

The password for authentication.

### Option: `download_dir`

The download location for files.

### Option: `incomplete_dir`

The download location for incomplete files.

### Option: `uitheme`

This addon has 5 Web UIs for Transmission. You can select one of these:
`default`, `transmission-web-control`, `combustion`, `kettu`,
`flood-for-transmission`

## Embedding into Home Assistant

This addon supports ingress, thus it can simply be integrated into Home
Assistant without having to forward any additional ports. Here is an example
configuration:

```yaml
transmission:
  host: f6fddefc-transmission
```

If you want, you can add an icon to the sidebar by toggling _Show in Sidebar_
as well.

## Changelog & Releases

This repository keeps a change log using [GitHub's releases][releases]
functionality.

Releases are based on [Semantic Versioning][semver], and use the format
of `MAJOR.MINOR.PATCH`. In a nutshell, the version will be incremented
based on the following:

- `MAJOR`: Incompatible or major changes.
- `MINOR`: Backwards-compatible new features and enhancements.
- `PATCH`: Backwards-compatible bugfixes and package updates.

## Support

Got questions?

You could [open an issue here][issue] GitHub.

## Authors & contributors

The original setup of this repository is by [Pierrick Rouxel][pierrick].
Web UIs added by [Barış Özdağ][barisozdag].

For a full list of all authors and contributors,
check [the contributor's page][contributors].

## License

MIT License

Copyright (c) 2018 Pierrick Rouxel, 2021-2024 Barış Özdağ

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

[addon-badge]: https://my.home-assistant.io/badges/supervisor_addon.svg
[addon]: https://my.home-assistant.io/redirect/supervisor_addon/?addon=bb761233_transmission
[contributors]: https://github.com/barisozdag/addon-transmission/graphs/contributors
[barisozdag]: https://github.com/barisozdag
[issue]: https://github.com/barisozdag/addon-transmission/issues
[pierrick]: https://github.com/pierrickrouxel
[releases]: https://github.com/barisozdag/addon-transmission/releases
[repository-badge]: https://my.home-assistant.io/badges/supervisor_add_addon_repository.svg
[repository]: https://my.home-assistant.io/redirect/supervisor_add_addon_repository/?repository_url=https%3A%2F%2Fgithub.com%2Fbarisozdag%2Fhaddons-repo
[semver]: https://semver.org/spec/v2.0.0.html
