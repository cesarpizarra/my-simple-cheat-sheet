## SSH Notes

### Creae SSH Key:

```bash
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

### Copy SSH Key:

- MacOS : `pbcopy < ~/.ssh/id_rsa.pub`
- Linux : `xclip -sel clip < ~/.ssh/id_rsa.pub`
- Windows : `clip < ~/.ssh/id_rsa.pub`
