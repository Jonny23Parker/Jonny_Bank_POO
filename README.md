# Jonny_Bank_POO
Modelando o Sistema Bancário em POO com Python _ DIO


o codigo ficou dessa forma abaixo.


# Modelando o Sistema Bancario com POO com Python!

class Cliente:
    def __init__(self, nome, telefone):
        self.nome = nome
        self.telefone = telefone

class Conta:
    def __init__(self, clientes, número, saldo=0):
        self.saldo = 0
        self.clientes = clientes
        self.número = número
        self.operações = []
        self.deposito(saldo)

    def resumo(self):
        print(f"CC N°{self.número} Saldo: {self.saldo:10,.2f}")

    def pode_sacar(self, valor):
        return self.saldo >= valor

    def saque(self, valor):
        if self.pode_sacar(valor):
            self.saldo -= valor
            self.operações.append(["SAQUE", valor])
            return True
        else:
            print("Saldo insuficiente!")
            return False

    def deposito(self, valor):
        self.saldo += valor
        self.operações.append(["DEPÓSITO", valor])

    def extrato(self):
        print(f"Extrato CC N° {self.número}\n")
        for o in self.operações:
            print(f"{o[0]:10s}   {o[1]:10,.2f}")
        print(f"\n      Saldo: {self.saldo:10,.2f}\n")


class ContaEspecial(Conta):
    def __init__(self, clientes, número, saldo=0, limite=0):
        Conta.__init__(self, clientes, número, saldo)
        self.limite = limite

    def pode_sacar(self, valor):
        return self.saldo + self.limite >= valor

    def extrato(self):
        Conta.extrato(self)
        print(f"\n     Limite: {self.limite:10,.2f}\n")
        print(f"\n Disponivel: {self.limite + self.saldo:10,.2f}\n")


Jonatas = Cliente("Jonatas", "2380-2612")

conta = ContaEspecial([Jonatas], 87563, 19000, 3000)
conta.extrato()
conta.saque(8000)
conta.saque(2500)
conta.saque(3500)
conta.extrato()
