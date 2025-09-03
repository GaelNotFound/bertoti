1. Comentário sobre o primeiro trecho:

  O trecho fala que engenharia de software vai além de programar, sendo sobre aplicar conhecimentos teóricos para criar sistemas confiáveis e seguros. À medida que o software cresce, é preciso organizar o código de forma a ser adaptável e escalável ao longo do tempo, levando em conta os custos e as mudanças.

2. Comentário sobre o segundo trecho:

  O segundo trecho menciona 3 trade-offs:

  Desempenho vs. Legibilidade: Melhorar o desempenho pode deixar o código mais difícil de entender.

  Velocidade de Desenvolvimento vs. Qualidade: Fazer rápido pode afetar a qualidade do código, com mais chances de erro.

  Escalabilidade vs. Simplicidade: Tornar o sistema escalável pode aumentar a complexidade, enquanto soluções simples podem não suportar o crescimento.

3. Exemplos de trade-offs:

  Desempenho vs. Consumo de Recursos: Melhorar o desempenho pode aumentar o uso de memória ou processamento.

  Desenvolvimento Rápido vs. Arquitetura Robusta: Entregar rápido pode prejudicar a estrutura do sistema, que ficará difícil de manter a longo prazo.

  Flexibilidade vs. Controle: Tornar o sistema flexível pode dificultar o controle sobre aspectos como segurança ou desempenho.

4. Diagrama de classe UML

   <img width="2816" height="1536" src="https://github.com/user-attachments/assets/6650a657-6fdb-4d1b-bdb4-8605620854c4" />
5. Java:
import java.util.ArrayList;
import java.util.Date;
import java.util.List;

/**
 * Classe Livro
 */
class Livro {
    private int idLivro;
    private String titulo;
    private String autor;
    private double preco;

    public Livro(int idLivro, String titulo, String autor, double preco) {
        this.idLivro = idLivro;
        this.titulo = titulo;
        this.autor = autor;
        this.preco = preco;
    }

    // Getters
    public int getIdLivro() { return idLivro; }
    public String getTitulo() { return titulo; }
    public String getAutor() { return autor; }
    public double getPreco() { return preco; }

    @Override
    public String toString() {
        return "Livro{" +
               "id=" + idLivro +
               ", titulo='" + titulo + '\'' +
               ", preco=" + String.format("%.2f", preco) +
               '}';
    }
}

/**
 * Classe ItemPedido
 */
class ItemPedido {
    private Livro livro;
    private int quantidade;
    private double precoUnitario;

    public ItemPedido(Livro livro, int quantidade) {
        this.livro = livro;
        this.quantidade = quantidade;
        this.precoUnitario = livro.getPreco(); // Preço no momento da compra
    }

    // Getters
    public Livro getLivro() { return livro; }
    public int getQuantidade() { return quantidade; }
    public double getPrecoUnitario() { return precoUnitario; }

    // Método para calcular o subtotal do item
    public double calcularSubtotal() {
        return this.quantidade * this.precoUnitario;
    }

    @Override
    public String toString() {
        return "ItemPedido{" +
               "livro=" + livro.getTitulo() +
               ", quantidade=" + quantidade +
               ", subtotal=" + String.format("%.2f", calcularSubtotal()) +
               '}';
    }
}

/**
 * Classe Pagamento
 */
class Pagamento {
    private int idPagamento;
    private Date data;
    private double valor;
    private String metodo; // Ex: "Cartão de Crédito", "Boleto"

    public Pagamento(int idPagamento, double valor, String metodo) {
        this.idPagamento = idPagamento;
        this.data = new Date(); // Data atual
        this.valor = valor;
        this.metodo = metodo;
    }

    public void confirmarPagamento() {
        System.out.println("Pagamento de R$ " + String.format("%.2f", valor) + " via " + metodo + " confirmado.");
    }

    @Override
    public String toString() {
        return "Pagamento{" +
               "id=" + idPagamento +
               ", data=" + data +
               ", valor=" + String.format("%.2f", valor) +
               ", metodo='" + metodo + '\'' +
               '}';
    }
}

/**
 * Classe Pedido
 */
class Pedido {
    private int idPedido;
    private Date data;
    private String status;
    private Cliente cliente;
    private List<ItemPedido> itens;
    private List<Pagamento> pagamentos;

    public Pedido(int idPedido, Cliente cliente) {
        this.idPedido = idPedido;
        this.cliente = cliente;
        this.data = new Date();
        this.status = "Aguardando Pagamento";
        this.itens = new ArrayList<>();
        this.pagamentos = new ArrayList<>();
    }
    
    // Getters
    public int getIdPedido() { return idPedido; }
    public List<ItemPedido> getItens() { return itens; }
    public String getStatus() { return status; }

    // Métodos de negócio
    public void adicionarItem(Livro livro, int quantidade) {
        ItemPedido novoItem = new ItemPedido(livro, quantidade);
        this.itens.add(novo
6. // Salve este arquivo como "SistemaVendas.java"

import java.util.ArrayList;
import java.util.Date;
import java.util.List;

/**
 * Classe Livro
 * Representa um livro com suas informações básicas.
 */
class Livro {
    private int idLivro;
    private String titulo;
    private String autor;
    private double preco;

    public Livro(int idLivro, String titulo, String autor, double preco) {
        this.idLivro = idLivro;
        this.titulo = titulo;
        this.autor = autor;
        this.preco = preco;
    }

    // Getters
    public int getIdLivro() { return idLivro; }
    public String getTitulo() { return titulo; }
    public String getAutor() { return autor; }
    public double getPreco() { return preco; }

    @Override
    public String toString() {
        return "Livro{" +
               "id=" + idLivro +
               ", titulo='" + titulo + '\'' +
               ", preco=" + String.format("%.2f", preco) +
               '}';
    }
}

/**
 * Classe ItemPedido
 * Representa a relação entre um Pedido e um Livro.
 */
class ItemPedido {
    private Livro livro;
    private int quantidade;
    private double precoUnitario;

    public ItemPedido(Livro livro, int quantidade) {
        this.livro = livro;
        this.quantidade = quantidade;
        this.precoUnitario = livro.getPreco(); // Preço no momento da compra
    }

    // Getters
    public Livro getLivro() { return livro; }
    public int getQuantidade() { return quantidade; }
    public double getPrecoUnitario() { return precoUnitario; }

    // Método para calcular o subtotal do item
    public double calcularSubtotal() {
        return this.quantidade * this.precoUnitario;
    }

    @Override
    public String toString() {
        return "ItemPedido{" +
               "livro=" + livro.getTitulo() +
               ", quantidade=" + quantidade +
               ", subtotal=" + String.format("%.2f", calcularSubtotal()) +
               '}';
    }
}

/**
 * Classe Pagamento
 * Representa um pagamento associado a um pedido.
 */
class Pagamento {
    private int idPagamento;
    private Date data;
    private double valor;
    private String metodo; // Ex: "Cartão de Crédito", "Boleto"

    public Pagamento(int idPagamento, double valor, String metodo) {
        this.idPagamento = idPagamento;
        this.data = new Date(); // Data atual
        this.valor = valor;
        this.metodo = metodo;
    }

    public void confirmarPagamento() {
        System.out.println("Pagamento de R$ " + String.format("%.2f", valor) + " via " + metodo + " confirmado.");
    }

    @Override
    public String toString() {
        return "Pagamento{" +
               "id=" + idPagamento +
               ", data=" + data +
               ", valor=" + String.format("%.2f", valor) +
               ", metodo='" + metodo + '\'' +
               '}';
    }
}

/**
 * Classe Pedido
 * A classe central que une clientes, livros e pagamentos.
 */
class Pedido {
    private int idPedido;
    private Date data;
    private String status;
    private Cliente cliente;
    private List<ItemPedido> itens;
    private List<Pagamento> pagamentos;

    public Pedido(int idPedido, Cliente cliente) {
        this.idPedido = idPedido;
        this.cliente = cliente;
        this.data = new Date();
        this.status = "Aguardando Pagamento";
        this.itens = new ArrayList<>();
        this.pagamentos = new ArrayList<>();
    }
    
    // Getters
    public int getIdPedido() { return idPedido; }
    public List<ItemPedido> getItens() { return itens; }
    public String getStatus() { return status; }

    // Métodos de negócio
    public void adicionarItem(Livro livro, int quantidade) {
        ItemPedido novoItem = new ItemPedido(livro, quantidade);
        this.itens.add(novo)
