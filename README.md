def encrypt(text, shift):
    result = ""

    for char in text:
        if char.isupper():
            result += chr((ord(char) + shift - 65) % 26 + 65)
        elif char.islower():
            result += chr((ord(char) + shift - 97) % 26 + 97)
        else:
            result += char

    return result


def decrypt(text, shift):
    return encrypt(text, -shift)


def brute_force_decrypt(cipher_text):
    print("\n🔍 Brute-force decryption (Trying all 25 shifts):\n")
    for shift in range(1, 26):
        possible_text = ""
        for char in cipher_text:
            if char.isupper():
                possible_text += chr((ord(char) - shift - 65) % 26 + 65)
            elif char.islower():
                possible_text += chr((ord(char) - shift - 97) % 26 + 97)
            else:
                possible_text += char
        print(f"Shift {shift:2}: {possible_text}")



if __name__ == "__main__":
    print("=== Caesar Cipher Tool ===")
    print("Choose an option:")
    print("  [E] Encrypt")
    print("  [D] Decrypt")
    print("  [B] Brute-force Decrypt")

    choice = input("Your choice: ").strip().lower()

    if choice == 'e':
        message = input("Enter your message to encrypt: ")
        shift = int(input("Enter the shift key (1-25): "))
        encrypted = encrypt(message, shift)
        print("🔐 Encrypted message:", encrypted)

    elif choice == 'd':
        message = input("Enter your message to decrypt: ")
        shift = int(input("Enter the shift key used (1-25): "))
        decrypted = decrypt(message, shift)
        print("🔓 Decrypted message:", decrypted)

    elif choice == 'b':
        message = input("Enter the encrypted message: ")
        brute_force_decrypt(message)

    else:
        print("❌ Invalid choice. Please select E, D, or B.")
