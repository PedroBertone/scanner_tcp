# scanner_tcp
Simple Scanner TCP Port

(basic)
import socket

def scan_port(ip, port):
    sock = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    sock.settimeout(1)  # Tempo limite para resposta
    try:
        sock.connect((ip, port))
        print(f"[+] Porta {port} está ABERTA")
    except:
        pass
    finally:
        sock.close()

# IP do alvo
target_ip = input("Digite o IP ou domínio a ser escaneado: ")

# Faixa de portas
for port in range(1, 1025):  # Portas bem conhecidas
    scan_port(target_ip, port)


With Treads (Faster)

import socket
import threading

def scan_port(ip, port):
    try:
        sock = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
        sock.settimeout(0.5)
        sock.connect((ip, port))
        print(f"[+] Porta {port} está ABERTA")
    except:
        pass
    finally:
        sock.close()

def main():
    target = input("Digite o IP ou domínio a ser escaneado: ")
    print(f"\n[+] Iniciando varredura em: {target}\n")

    for port in range(1, 1025):
        thread = threading.Thread(target=scan_port, args=(target, port))
        thread.start()

if __name__ == "__main__":
    main()

