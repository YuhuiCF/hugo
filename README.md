# hugo

My hugo repository to host my blogs.

[Online version](https://yuhuix.github.io/hugo/)

## Development

To edit and preview with hugo:

```bash
hugo server
# or npm run serve
```

Update the value `lastmod` with help of the hugos auto-refresh feature.

To generate the site (should be included in the release commands):

```bash
rm -rf ./docs
hugo
# or npm run dist
```

## Release

Instructions:

1. `npm run dist`
2. `node ./node_modules/version-patch/ --commit X.Y.Z`
3. `node ./node_modules/version-patch/ --tag X.Y.Z`
4. `git push`
5. `git push --tags`

The version number shall be used as:

- Major X: breaking changes, framework changes
- Minor Y: New post, feature
- Patch Z: post updates
