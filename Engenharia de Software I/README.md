# Atividades Bertoti

1. Engenharia de software implica mais na aplicação de conhecimentos teóricos de construçaõ de software do que a programação em si. Conforme o desenvolvimento de softwares evolui, devemos criar métodos e padrões de engenharia mais rigorosos para garantir a segurança e confiabilidade.


2. O parágrafo reflete sobre a engenharia de software, e apresennta princípios para garantir a organização dos códigos, sendo: <b>Tempo e Mudança:</b> Como o código precisará se adaptar ao longo de sua vida, <b>Escala e Crescimento:</b> Como a organização precisará se adaptar à medida que evolui, <b>Compensações e Custos:</b> Como a organização toma decisões, com base nas lições de Tempo e Mudança, e Escala e Crescimento.


3. A) Desempenho vs. Legibilidade do Código  
   Explicação: Melhorar o desempenho pode resultar em código mais difícil de entender, o que torna a manutenção mais difícil.

   B) 2. Velocidade de Desenvolvimento vs. Qualidade do Código   
   Explicação: Entregar rapidamente pode sacrificar a qualidade do código, como testes e boas práticas, o que aumenta o risco de erros.

   C) 3. Escalabilidade vs. Simplicidade  
   Explicação: Soluções escaláveis exigem mais complexidade, mas tornam o sistema mais preparado para crescer. Soluções simples podem não suportar o aumento de usuários ou dados.


4. Diagrama de Classes UML
<img src="https://github.com/DanielDPereira/bertoti/blob/main/Engenharia%20de%20Software%20I/diagramaClassesUML2808.png?raw=true"/>

5. Java:
```java
import java.util.ArrayList;
import java.util.List;
import java.text.SimpleDateFormat;
import java.util.Date;

public class SistemaBancario {

    // Classe Cliente
    static class Cliente {
        private String nome;
        private String cpf;
        private List<ContaBancaria> contas;

        public Cliente(String nome, String cpf) {
            this.nome = nome;
            this.cpf = cpf;
            this.contas = new ArrayList<>();
        }

        public void abrirConta(ContaBancaria conta) {
            contas.add(conta);
            System.out.println("Conta aberta para " + nome + " com sucesso.");
        }

        public void fecharConta(ContaBancaria conta) {
            if (contas.contains(conta)) {
                contas.remove(conta);
                System.out.println("Conta fechada com sucesso.");
            } else {
                System.out.println("Conta não encontrada.");
            }
        }

        public List<ContaBancaria> getContas() {
            return contas;
        }
    }

    // Classe ContaBancaria
    static class ContaBancaria {
        private String numeroConta;
        private double saldo;
        private String tipo;

        public ContaBancaria(String numeroConta, String tipo) {
            this.numeroConta = numeroConta;
            this.saldo = 0.0;
            this.tipo = tipo;
        }

        public void depositar(double valor) {
            if (valor > 0) {
                saldo += valor;
                System.out.println("Depósito de " + valor + " realizado com sucesso.");
            } else {
                System.out.println("Valor inválido para depósito.");
            }
        }

        public void sacar(double valor) {
            if (valor <= saldo && valor > 0) {
                saldo -= valor;
                System.out.println("Saque de " + valor + " realizado com sucesso.");
            } else {
                System.out.println("Saldo insuficiente ou valor inválido.");
            }
        }

        public void transferir(ContaBancaria contaDestino, double valor) {
            if (valor <= saldo && valor > 0) {
                this.saldo -= valor;
                contaDestino.depositar(valor);
                System.out.println("Transferência de " + valor + " realizada com sucesso.");
            } else {
                System.out.println("Saldo insuficiente ou valor inválido.");
            }
        }

        public double getSaldo() {
            return saldo;
        }

        public String getNumeroConta() {
            return numeroConta;
        }

        public String getTipo() {
            return tipo;
        }
    }

    // Classe Transacao
    static class Transacao {
        private String tipo;
        private double valor;
        private String data;
        private ContaBancaria contaOrigem;
        private ContaBancaria contaDestino;

        public Transacao(String tipo, double valor, ContaBancaria contaOrigem, ContaBancaria contaDestino) {
            this.tipo = tipo;
            this.valor = valor;
            this.contaOrigem = contaOrigem;
            this.contaDestino = contaDestino;
            this.data = new SimpleDateFormat("dd/MM/yyyy HH:mm:ss").format(new Date());
        }

        public void registrar() {
            System.out.println("Transação registrada: ");
            System.out.println("Tipo: " + tipo);
            System.out.println("Valor: " + valor);
            System.out.println("Data: " + data);
            if (contaOrigem != null) {
                System.out.println("Conta Origem: " + contaOrigem.getNumeroConta());
            }
            if (contaDestino != null) {
                System.out.println("Conta Destino: " + contaDestino.getNumeroConta());
            }
        }
    }

    // Método main para rodar o sistema
    public static void main(String[] args) {
        // Criando clientes
        Cliente cliente1 = new Cliente("João Silva", "123.456.789-00");

        // Criando contas bancárias
        ContaBancaria conta1 = new ContaBancaria("12345", "Corrente");
        ContaBancaria conta2 = new ContaBancaria("67890", "Poupança");

        // Abrindo contas para o cliente
        cliente1.abrirConta(conta1);
        cliente1.abrirConta(conta2);

        // Depositando dinheiro nas contas
        conta1.depositar(1000);
        conta2.depositar(500);

        // Realizando transações
        conta1.sacar(200);
        conta1.transferir(conta2, 300);

        // Registrando transações
        Transacao t1 = new Transacao("Saque", 200, conta1, null);
        t1.registrar();

        Transacao t2 = new Transacao("Transferência", 300, conta1, conta2);
        t2.registrar();
    }
}

```
6. Testes:
```
import static org.junit.jupiter.api.Assertions.assertEquals;

import org.junit.jupiter.api.Test;

public class SistemaBancarioTest {

    @Test
    void testDeposito() {
        SistemaBancario.ContaBancaria conta = new SistemaBancario.ContaBancaria("12345", "Corrente");
        conta.depositar(1000);
        assertEquals(1000, conta.getSaldo());
    }

    @Test
    void testSaque() {
        SistemaBancario.ContaBancaria conta = new SistemaBancario.ContaBancaria("12345", "Corrente");
        conta.depositar(1000);
        conta.sacar(200);
        assertEquals(800, conta.getSaldo());
    }

    @Test
    void testTransferencia() {
        SistemaBancario.ContaBancaria conta1 = new SistemaBancario.ContaBancaria("12345", "Corrente");
        SistemaBancario.ContaBancaria conta2 = new SistemaBancario.ContaBancaria("67890", "Poupança");

        conta1.depositar(1000);
        conta1.transferir(conta2, 300);

        assertEquals(700, conta1.getSaldo()); // saldo da conta origem
        assertEquals(300, conta2.getSaldo()); // saldo da conta destino
    }
}

```

7. Diagrama de Classes UML
</h>
<div style="background-color: rgba(22, 44, 37, 1); padding: 10px; border: 2px solid rgba(0, 236, 146, 1); border-radius: 10px; margin-bottom: 30px">
      <img src="https://raw.githubusercontent.com/KauanDomingues/bertoti/refs/heads/main/engenhariadesoftware/image-2.png" alt="colmeia-modelo-logico"style="filter: invert(1);">
</div>

<h style="background-color: rgba(22, 44, 37, 1); padding: 10px; z-index: -1; border-radius: 20px; border: 2px solid rgba(0, 236, 146, 1); border-bottom: none; margin-left: 20px;">
8. Java
</h>
<div style="background-color: rgba(22, 44, 37, 1); padding: 35px; border: 2px solid rgba(0, 236, 146, 1); border-radius: 10px; margin-bottom: 30px; overflow-x: auto;">

<div style="display: inline-flex; flex-wrap: no-wrap; gap: 10px;">
<div style="width: 70vw;">

      public class Obra {

            private String titulo;
            private String autor;
            private List<Integer> avaliacoes = new ArrayList<>();
            private double avaliacoesMedia;

            // Construtor
            public Obra(String titulo, String autor) {
                  this.titulo = titulo;
                  this.autor = autor;
            }

            // Getters e Setters
            public String getTitulo() { return titulo; }
            public void setTitulo(String titulo) { this.titulo = titulo; }

            public String getAutor() { return autor; }
            public void setAutor(String autor) { this.autor = autor; }

            public List<Integer> getAvaliacoes() { return avaliacoes; }
            public void setAvaliacoes(List<Integer> avaliacoes) { this.avaliacoes = avaliacoes; }

            public double getAvaliacoesMedia() { return avaliacoesMedia; }
            public void setAvaliacoesMedia(double avaliacoesMedia) { this.avaliacoesMedia = avaliacoesMedia; }

            // Adiciona nova avaliação e atualiza média
            public void adicionarAvaliacao(int novaAvaliacao) {
                  avaliacoes.add(novaAvaliacao);
                  setAvaliacoesMedia(atualizarAvaliacoesMedia());
            }

            // Calcula a média das avaliações
            public double atualizarAvaliacoesMedia() {
                  double soma = 0.0;
                  for (int num : avaliacoes) {
                        soma += num;
                  }
                  return soma / avaliacoes.size();
            }
      }
</div>

<div>

<div style="width: 70vw;">    

      public class Critico {
            private String nome;
            
            public Critico(String nome){this.nome = nome;}

            public void avaliarObra(Obra obra, int avaliacao){obra.adicionarAvaliacao(avaliacao);}
      }
</div>

<div style="width: 70vw">

      public class Museu {
            private String nome;
            private List<Obra> obras= new ArrayList<>();
            private double estrelas = 0.0;

            public String getNome() {return nome;}
            public void setNome(String nome) {this.nome = nome;}

            public List<Obra> getObras() {return obras;}
            public void setObras(List<Obra> obras) {this.obras = obras;}

            public double getEstrelas() {return estrelas;}
            public void setEstrelas(double estrelas) {this.estrelas = estrelas;}

            public Museu(String nome) {this.nome = nome;}

            public void adicionarObra(Obra obra){obras.add(obra);}

            public void atualizarEstrelas(){
                  double avaliacoesMedia = this.obras.stream().mapToDouble(Obra::getAvaliacoesMedia).sum();
                  setEstrelas(avaliacoesMedia);
            }
      }
</div>
</div>
</div>
</div>

<h style="background-color: rgba(22, 44, 37, 1); padding: 10px; z-index: -1; border-radius: 20px; border: 2px solid rgba(0, 236, 146, 1); border-bottom: none; margin-left: 20px;">
9.Testes Automatizados
</h>
<div style="background-color: rgba(22, 44, 37, 1); padding: 30px; border: 2px solid rgba(0, 236, 146, 1); border-radius: 10px; margin-bottom: 30px">

<div>

      import org.junit.jupiter.api.Test;
      import static org.junit.jupiter.api.Assertions.assertEquals;

      class MuseuTest {
            @Test
            void test(){
                  Museu museu = new Museu("Museu1");

                  Obra obra1 = new Obra("Obra1", "Autor1");
                  Obra obra2 = new Obra("Obra2", "Autor2");
                  Obra obra3 = new Obra("Obra3", "Autor3");

                  museu.adicionarObra(obra1);
                  museu.adicionarObra(obra2);
                  museu.adicionarObra(obra3);

                  Critico critico1 = new Critico("Critico1");
                  Critico critico2 = new Critico("Critico2");
                  Critico critico3 = new Critico("Critico3");

                  critico1.avaliarObra(obra1, 4);
                  critico1.avaliarObra(obra2, 1);
                  critico1.avaliarObra(obra3, 5);
                  critico2.avaliarObra(obra1, 4);
                  critico2.avaliarObra(obra2, 5);
                  critico2.avaliarObra(obra3, 5);
                  critico3.avaliarObra(obra1, 1);
                  critico3.avaliarObra(obra2, 2);
                  critico3.avaliarObra(obra3, 5);

                  museu.atualizarEstrelas();

                  assertEquals(3.0, obra1.getAvaliacoesMedia());
                  assertEquals(8.0/3, obra2.getAvaliacoesMedia());
                  assertEquals(5.0, obra3.getAvaliacoesMedia());
                  assertEquals(32.0/3, museu.getEstrelas());
            }
      }
</div>


</div>

