# Extract Secret Text from Image

## Overview

This Python script, `extract_secret_text.py`, extracts a hidden message from an image file. The hidden message is embedded in the least significant bits of the image file's pixel data. The script follows a process of reading the image, extracting bits based on an algorithm, converting those bits into bytes, and finally writing the extracted secret message to a text file.

## How It Works

The script works by reading a BMP image file (`flower_with_text.bmp`) that contains a hidden message in its pixel data. The message is hidden by modifying the least significant bit (LSB) of some of the image's bytes. The script reverses this process by reading those least significant bits, assembling them into bytes, and outputting the hidden message.

### Key Steps:
1. **Read Image Data:**
   - Opens the image file as binary data and reads the entire byte array.
   
2. **Extract Hidden Bits:**
   - Using the values of `p` and `q`, the script starts at the header length (54 bytes) and extracts bits from the image data by taking the least significant bit of specific bytes.

3. **Convert Bits to Bytes:**
   - The extracted bits are grouped into bytes to form the hidden message.

4. **Write Output:**
   - The assembled bytes (i.e., the hidden message) are written to a file named `hidden_text_we_found.txt`.

## Script Breakdown

### Functions:

1. **`est_extract()`**
   - Main function that coordinates the extraction process. It calls the helper functions to:
     - Get the byte array of the image.
     - Extract the hidden bits from the image.
     - Convert those bits into a byte array.
     - Write the final extracted text to a file.

2. **`est_get_bytes_containing_message()`**
   - Opens and reads the BMP image file, returning its byte array.

3. **`est_extract_bits_from_image(data, header_len, p, q)`**
   - Extracts the least significant bits from the image data using the parameters `p` and `q` which determine the positions from which to extract the bits.

4. **`est_convert_bits_to_bytes(text_as_bits)`**
   - Converts the array of extracted bits into an array of bytes, which represents the hidden message.

5. **`est_write_message_text(text)`**
   - Writes the extracted hidden message (byte array) to an output file `hidden_text_we_found.txt`.

## Usage

### Prerequisites:
- Python 3.x
- A BMP image file (`flower_with_text.bmp`) that contains the hidden message.

### Steps to Run:
1. Place the BMP image file (`flower_with_text.bmp`) in the same directory as the script.
2. Run the script from the command line:
   ```bash
   python est_extract_secret_text.py
   ```
3. The extracted message will be written to a file named hidden_text_we_found.txt in the same directory.
## Notes
The script assumes the image uses a BMP file format. For other image formats, the script would need to be modified.
The hidden message is stored in the least significant bit (LSB) of the image data. The script only extracts the hidden message by reading these LSBs.
This technique is known as steganography – the practice of concealing messages or information within other non-secret text or data.
