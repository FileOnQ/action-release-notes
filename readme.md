# Introduction
The propose of the action is to publish the changelog and release notes for a release using Gren.

# Usage

Configure Gren using `.grenrc` in your repository and run this action in GitHub actions workflow.

## Example Gren File

```javascript
module.exports = {
    "dataSource": "issues",
    "prefix": "",
    "onlyMilestones": false,
    "ignoreIssuesWith": [
		"duplicate",
		"invalid",
		"question",
		"wontfix"
	],
    "groupBy": {
        "⚒ Enhancements": ["⚒ Enhancement"],
		"🔧 Native Changes (C++)": [ "🔧 Native" ],
        "⚙ Build & DevOps": ["⚙ DevOps" ],
        "🐛 Bugs Fixed:": ["🐛 Bug"],
        "🧪 Testing and Samples": ["🧪 Testing"],
        "📓 Documentation Improvements:": ["📓 Documentation" ]
    },
    "changelogFilename": "CHANGELOG.md",
    "template": {
        commit: ({ message, url, author, name }) => `- [${message}](${url}) - ${author ? `@${author}` : name}`,
        issue: "- [{{text}}]({{url}}) {{name}}",
        label: "[**{{label}}**]",
        noLabel: "closed",
        group: "\n#### {{heading}}\n",
        changelogTitle: "# Changelog\n\n",
        release: "## {{release}} ({{date}})\n{{body}}",
        releaseSeparator: "\n---\n\n"
    }
}
```

## Example Github Actions YML

```yaml
  uses: FileOnQ/action-release-notes@v1.2
  with:
    token : GITHUB_TOKEN_THAT_HAS_PERMISSIONS
    username : USERNAME
    organization : 'FileOnQ'
    repository : 'Imaging.Heif'
    version_number : PACKAGE_VERSION
    options: '--override --ignore-tags-with="preview"'
```
