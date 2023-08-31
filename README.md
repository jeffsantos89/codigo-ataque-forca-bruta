# codigo-ataque-forca-bruta
código feito para ataque e quebra de senhas feito em sh. pode ser usado para ataque em portas,ou em sistemas operacionais.
#!/bin/bash

echo "Teste de Força Bruta"
echo -n "Informe uma senha > "
read password

python3 - <<END
import time

class Cracker:
    def __init__(self):
        self.first_char = ord('a')
        self.last_char = ord('z')
        self.attempts = 0
        self.completed = False
        self.password = ""

    def crack_password(self, keys):
        if keys == self.password:
            self.completed = True
        if len(keys) == len(self.password) or self.completed:
            return
        for char in range(self.first_char, self.last_char + 1):
            self.attempts += 1
            self.crack_password(keys + chr(char))

if __name__ == "__main__":
    password = "$password".lower()
    
    cracker = Cracker()
    cracker.password = password
    
    print("\nQuebrando a senha...")
    start_time = time.time()

    cracker.crack_password("")

    end_time = time.time()
    elapsed_time = end_time - start_time
    
    if elapsed_time > 0:
        print("\n\nA senha foi hackeada! Estatísticas:")
        print("----------------------------------")
        print(f"Password: {cracker.password}")
        print(f"Tamanho Senha: {len(cracker.password)}")
        print(f"Tentativas: {cracker.attempts}")
        plural = "segundos" if elapsed_time != 1 else "segundo"
        print(f"Tempo gasto para hackear a senha: {elapsed_time:.2f} {plural}")
        print(f"Senhas por segundo: {int(cracker.attempts / elapsed_time)}")
    else:
        print("\n\nA senha foi hackeada! Estatísticas:")
        print("----------------------------------")
        print(f"Senha: {cracker.password}")
        print(f"Tamanho da Senha: {len(cracker.password)}")
        print(f"Tentativas: {cracker.attempts}")
        print(f"Tempo para hackear: {elapsed_time:.2f} segundos")
END