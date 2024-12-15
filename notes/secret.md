## Creating a secret key

Open your terminal or command prompt.
Run the following Node.js script to generate a random string:

```bash
node -e "console.log(require('crypto').randomBytes(32).toString('hex'))"
```

This command uses the crypto module in Node.js to generate a random sequence of 32 bytes and then converts it to a hexadecimal string.
