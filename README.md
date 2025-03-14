# TERMHOOK

Termhook is a command-line tool that allows you to send messages to Discord using a webhook in a terminal and get ID of message.
Send or Update message with raw texte, code blocks, and embeds.
Include ANSI code block formatting support for text color, background color, bold, underline with easy syntax.

## Usage
```bash
termhook -w <webhook_url> [-i <message_id> -c <block_code> -e] <message/json embed>
```

## Options
```bash
Usage: termhook -w <webhook> [OPTIONS] <message>
<message> must be less than 2000 characters.

Options:
  -w          Webhook full URL or ID/TOKEN(?thread_id=ID). [required]
  -i          Message ID to update. [optional]
  -c          Code block language (bash, python, ansi, etc.). [optional]
              ANSI tags are supported:
                [t...]: Text color
                [tb...]: Bold text color
                [tu...]: Underlined text color
                [bg...]: Background color
                [r]: Reset
              Available colors: gray/grey, red, green, yellow, blue, pink, cyan, white, black

  -e          Embed message (json structure necessary on <message>). [optional]

  -h          Display this usage message.
```

## Examples send message
### Raw Text + Full URL
```bash
termhook -w https://discord.com/api/webhooks/1234567890/webhook_token "Hello, World!"
```
### Code Block + Short URL (/!\ need to escape quotes)
```bash
termhook -w /1234567890/webhook_token -c bash "echo \"Hello, World!\""
```
### Embed + Short URL with thread (/!\ need to escape quotes, exclamation, backtick)
```bash
termhook -w /1234567890/webhook_token?thread_id=9876543210 -e "{\"username\":\"Webhook\",\"avatar_url\":\"https://i.imgur.com/4M34hi2.png\",\"content\":\"Text message. Up to 2000 characters.\",\"embeds\":[{\"author\":{\"name\":\"Birdie♫\",\"url\":\"https://www.reddit.com/r/cats/\",\"icon_url\":\"https://i.imgur.com/R66g1Pe.jpg\"},\"title\":\"Title\",\"url\":\"https://google.com/\",\"description\":\"Text message. You can use Markdown here. *Italic* **bold** __underline__ ~~strikeout~~ [hyperlink](https://google.com) \`code\`\",\"color\":15258703,\"fields\":[{\"name\":\"Text\",\"value\":\"More text\",\"inline\":true},{\"name\":\"Even more text\",\"value\":\"Yup\",\"inline\":true},{\"name\":\"Use \`\\\"inline\\\": true\` parameter, if you want to display fields in the same line.\",\"value\":\"okay...\"},{\"name\":\"Thanks\\\!\",\"value\":\"You're welcome :wink:\"}],\"thumbnail\":{\"url\":\"https://upload.wikimedia.org/wikipedia/commons/3/38/4-Nature-Wallpapers-2014-1_ukaavUI.jpg\"},\"image\":{\"url\":\"https://upload.wikimedia.org/wikipedia/commons/5/5a/A_picture_from_China_every_day_108.jpg\"},\"footer\":{\"text\":\"Woah\\\! So cool\\\! :smirk:\",\"icon_url\":\"https://i.imgur.com/fKL31aD.jpg\"}}]}"
```
## Examples update message
### Raw Text + Message ID
```bash
termhook -w 1234567890/webhook_token -i 9876543210 "Hello, Everyone!"
```
### Code Block + Message ID
<img width="1061" alt="ansi-color" src="https://github.com/user-attachments/assets/3cbd97b7-b4f3-4518-84b2-9228b3aaa580" />

```bash
termhook -w https://discord.com/api/webhooks/1234567890/webhook_token -i 9876543210 -c bash "echo \"Hello, Everyone!\""
```
### Embed + Message ID
```bash
termhook -w https://discord.com/api/webhooks/1234567890/webhook_token?thread_id=9876543210 -e "{\"username\":\"Webhook UPDATED\",\"avatar_url\":\"https://i.imgur.com/4M34hi2.png\",\"content\":\"Text message updated. Up to 2000 characters.\",\"embeds\":[{\"author\":{\"name\":\"Birdie♫\",\"url\":\"https://www.reddit.com/r/cats/\",\"icon_url\":\"https://i.imgur.com/R66g1Pe.jpg\"},\"title\":\"Title\",\"url\":\"https://google.com/\",\"description\":\"Text message updated. You can use Markdown here. *Italic* **bold** __underline__ ~~strikeout~~ [hyperlink](https://google.com) \`code\`\",\"color\":15258703,\"fields\":[{\"name\":\"Text\",\"value\":\"More text\",\"inline\":true},{\"name\":\"Even more text\",\"value\":\"Yup\",\"inline\":true},{\"name\":\"Use \`\\\"inline\\\": true\` parameter, if you want to display fields in the same line.\",\"value\":\"okay...\"},{\"name\":\"Thanks\\\!\",\"value\":\"You're welcome :wink:\"}],\"thumbnail\":{\"url\":\"https://upload.wikimedia.org/wikipedia/commons/3/38/4-Nature-Wallpapers-2014-1_ukaavUI.jpg\"},\"image\":{\"url\":\"https://upload.wikimedia.org/wikipedia/commons/5/5a/A_picture_from_China_every_day_108.jpg\"},\"footer\":{\"text\":\"Woah\\\! So cool\\\! :smirk:\",\"icon_url\":\"https://i.imgur.com/fKL31aD.jpg\"}}]}"
```
## Example for use ANSI code block


### Syntax color
| COLOR                       | TEXT      | BOLD      | UNDERLINE | BACKGROUND |
|-----------------------------|-----------|-----------|-----------|------------|
| $${\color{grey}gray/grey}$$ | [tgray]   | [tbgray]  | [tugray]  | [bggray]   |
| $${\color{red}Red}$$        | [tred]    | [tbred]   | [tured]   | [bgred]    |
| $${\color{green}green}$$      | [tgreen]  | [tbgreen] | [tugreen] | [bggreen]  |
| $${\color{yellow}yellow}$$     | [tyellow] | [tbyellow]| [tuyellow]| [bgyellow] |
| $${\color{blue}blue}$$       | [tblue]   | [tbblue]  | [tublue]  | [bgblue]   |
| $${\color{pink}pink}$$       | [tpink]   | [tbpink]  | [tupink]  | [bgpink]   |
| $${\color{cyan}cyan}$$       | [tcyan]   | [tbcyan]  | [tucyan]  | [bgcyan]   |
| $${\color{white}white}$$      | [twhite]  | [tbwhite] | [tubyte]  | [bgwhite]  |
| $${\color{black}black}$$      | [tblack]  | [tbblack] | [tublack] | [bgblack]  |

```bash
termhook -w "1234567890/token" -c ansi " ·--------------------------------------------------·\n |   COLOR   | TEXT | BOLD | UNDERLINE | BACKGROUND |\n |-----------+------+------+-----------+------------|\n | gray/grey | [tgray]TEXT[r] | [tbgray]BOLD[r] | [tugray]UNDERLINE[r] | [bggray]BACKGROUND[r] |\n | red       | [tred]TEXT[r] | [tbred]BOLD[r] | [tured]UNDERLINE[r] | [bgred]BACKGROUND[r] |\n | green     | [tgreen]TEXT[r] | [tbgreen]BOLD[r] | [tugreen]UNDERLINE[r] | [bggreen]BACKGROUND[r] |\n | yellow    | [tyellow]TEXT[r] | [tbyellow]BOLD[r] | [tuyellow]UNDERLINE[r] | [bgyellow]BACKGROUND[r] |\n | blue      | [tblue]TEXT[r] | [tbblue]BOLD[r] | [tublue]UNDERLINE[r] | [bgblue]BACKGROUND[r] |\n | pink      | [tpink]TEXT[r] | [tbpink]BOLD[r] | [tupink]UNDERLINE[r] | [bgpink]BACKGROUND[r] |\n | cyan      | [tcyan]TEXT[r] | [tbcyan]BOLD[r] | [tucyan]UNDERLINE[r] | [bgcyan]BACKGROUND[r] |\n | white     | [twhite]TEXT[r] | [tbwhite]BOLD[r] | [tuwhite]UNDERLINE[r] | [bgwhite]BACKGROUND[r] |\n | black     | [tblack]TEXT[r] | [tbblack]BOLD[r] | [tublack]UNDERLINE[r] | [bgblack]BACKGROUND[r] |\n ·--------------------------------------------------·"
```
