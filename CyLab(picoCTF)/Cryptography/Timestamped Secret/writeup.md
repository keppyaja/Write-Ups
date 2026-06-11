# CTF Write-Up: picoCTF - timestamp

**Author:** Muhammad Tsaqif Fawwaz Nasywan (3125600010)  
**Category:** Cryptography  
**Platform:** picoCTF  

---

## Deskripsi Tantangan
Pada tantangan ini, kita diminta untuk mendekripsi sebuah pesan rahasia yang dienkripsi menggunakan algoritma AES dalam mode ECB. Pembuat soal meninggalkan celah keamanan yang fatal: kunci (*key*) enkripsinya tidak dibuat secara acak, melainkan menggunakan waktu sistem (*timestamp*).

## Analisis Kerentanan (Vulnerability)
Berdasarkan potongan kode pada file `encryption.py`, kita dapat mengamati bagaimana proses enkripsi dilakukan:

```python
timestamp = int(time.time())
key = sha256(str(timestamp).encode()).digest()[:16]
cipher = AES.new(key, AES.MODE_ECB)