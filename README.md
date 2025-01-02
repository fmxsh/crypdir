# crypdir - Directory Encryption and Decryption Script

This script provides a simple way to encrypt and compress directories or decrypt and decompress files using AES-256 encryption with OpenSSL. It supports both operations via command-line flags.

## Features

- **Encrypt (-e):** Compresses and encrypts a directory into a secure `.tar.gz.enc` file.
- **Decrypt (-d):** Decrypts and decompresses an `.enc` file into a directory.
- Customizable PBKDF2 iterations for enhanced security.
- Password input can be provided interactively or piped.

## Requirements

- `openssl`: Used for AES-256 encryption/decryption.
- `tar`: Used for compression and decompression.

## Usage

### Command Syntax

```bash
./script.sh [-d|-e] [--iter <iterations>] <source> <target>
```

### Options

- `-d`: Decrypt and decompress an encrypted file.
- `-e`: Encrypt and compress a directory.
- `-b`: The piped password is encoded with base64. This option decodes it with `base64 -d -w 0`.
- `-i <iterations>`: Number of PBKDF2 iterations (default: 1000). Increase for stronger key derivation security.
- `<source>`: Source file (encrypted file for `-d`, directory for `-e`).
- `<target>`: Target directory (for `-d`) or output file (for `-e`).

### Examples

#### Encrypt a Directory

```bash
./script.sh -e -i 2000 my_directory output_file.tar.gz.enc
```

- Compresses `my_directory` and encrypts it into `output_file.tar.gz.enc`.
- Uses 2000 PBKDF2 iterations.

#### Decrypt a File

```bash
./script.sh -d -i 2000 encrypted_file.tar.gz.enc target_directory
```

- Decrypts and decompresses `encrypted_file.tar.gz.enc` into `target_directory`.
- Uses 2000 PBKDF2 iterations.

### Password Handling

- If data is piped into the script, the password is read from the pipe.
- If not, the script prompts for a password interactively.

## Security Note

- Use a strong, memorable password.
- Consider increasing the PBKDF2 iteration count (`-i`) for higher security.
- Ensure encrypted files are stored securely to prevent unauthorized access.
