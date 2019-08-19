## trim whitespace
i like my editor to trim whitespace.
the only problem i have is with markdown files, where whitespace at the end is used for a newline.
to workaround the problem i added this in vscode settings.json

    "files.trimTrailingWhitespace": true,
    "[markdown]": {
        "files.trimTrailingWhitespace": false
    }

参考链接: https://github.com/editorconfig/editorconfig-vscode/issues/153