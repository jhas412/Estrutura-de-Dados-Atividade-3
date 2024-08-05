/*
UFPB - Universidade Federal da Paraíba
Curso: Ciências da Computação
Aluno: João Henrique Alves de Sousa
Matricula: 20230012690
Disciplina: Estrutura de dados
Professor Gilberto Farias
Período: 2024.1
Atividade 3 Estrutura lista encadeada
*/
package testeestruturalistaencadeada;

import java.util.Scanner;

public class TesteEstruturaListaEncadeada {

    public static class No {
        private int conteudo;
        private No proximo;

        public No() {
            this.proximo = null;
        }

        public int getConteudo() {
            return conteudo;
        }

        public void setConteudo(int conteudo) {
            this.conteudo = conteudo;
        }

        public No getProximo() {
            return proximo;
        }

        public void setProximo(No proximo) {
            this.proximo = proximo;
        }
    }

    public static class Lista {
        private No cabeça;
        private int tamanho;

        public Lista() {
            this.cabeça = null;
            this.tamanho = 0;
        }

        public boolean listaVazia() {  // Verifica se a lista está vazia
            return this.tamanho == 0;
        }

        public int tamanho() {  // Obtem o tamanho da lista
            return this.tamanho;
        }

        public int posiçãoDeElemento(int pos) {  // Obtem o valor do elemento na posição determinada
            No aux = cabeça;
            int cont = 1;

            if (listaVazia() || (pos < 1) || (pos > tamanho)){
                System.out.println("Lista vazia ou posicao invalida, retorna erro!!!");
                return -1;
            }
            while (cont < pos){
                aux = aux.getProximo();
                cont++;
            }
            return aux.getConteudo();
        }
        

        public int modificarValorDeElemento(int pos, int novoValor) {  // Modifica o valor do elemento na posição determinada
            No aux = cabeça;
            int cont = 1;

            if (listaVazia() || (pos < 1) || (pos > tamanho)){
                System.out.println("Lista vazia ou posicao invalida, retorna erro!!!");
                return -1;
            }
            while (cont < pos) {
                aux = aux.getProximo();
                cont++;
            }
            aux.setConteudo(novoValor);
            return aux.getConteudo();
        }

        

        public int inserirNaLista(int pos, int novoValor) {  // Inserir elementos na lista
            if (pos <= 0 || pos > tamanho + 1) {
                System.out.println("Lista vazia ou posicao invalida, retorna erro!!!");
                return -1;
            }

            No novoNo = new No();
            novoNo.setConteudo(novoValor);

            if (pos == 1) {                                 // No início
                novoNo.setProximo(cabeça);
                cabeça = novoNo;
            } else {
                No atual = cabeça;
                for (int i = 1; i < pos - 1; i++) {
                    atual = atual.getProximo();
                }
                novoNo.setProximo(atual.getProximo());
                atual.setProximo(novoNo);
            }

            tamanho++;
            return 1;
        }

        public int removerNaLista(int pos) {               // Remove elementos da lista encadeada
            if (listaVazia() || pos <= 0 || pos > tamanho) {
                System.out.println("Lista vazia ou posicao invalida, retorna erro!!!");
                return -1;
            }

            if (pos == 1) {                                 // No início
                No p = cabeça;
                int dado = p.getConteudo();
                cabeça = p.getProximo();
                tamanho--;
                return dado;
            } else {                                        // No meio ou no fim
                No atual = cabeça;
                No anterior = null;
                for (int i = 1; i < pos; i++) {
                    anterior = atual;
                    atual = atual.getProximo();
                }
                int dado = atual.getConteudo();
                anterior.setProximo(atual.getProximo());
                tamanho--;
                return dado;
            }
        }

        public void imprimirLista() {
            if (tamanho == 0) {
                System.out.println("Lista vazia");
            } else {
                No atual = cabeça;
                System.out.print("Lista = {");
                while (atual != null) {
                    System.out.print(atual.getConteudo());
                    atual = atual.getProximo();
                    if (atual != null) {
                        System.out.print(", ");
                    }
                }
                System.out.println("}");
            }
        }
        
        public void inserirElementosNaLista(int pos, int novoValor) {  // Inserir os elementos do vetor na lista
            No novoNo = new No();
            novoNo.setConteudo(novoValor);

            if (pos == 0) {
                novoNo.setProximo(cabeça);
                cabeça = novoNo;
            } else {
                No atual = cabeça;
                int indice = 0;
                while (atual != null && indice < pos - 1) {
                    atual = atual.getProximo();
                    indice++;
                }

                if (atual != null) {
                    novoNo.setProximo(atual.getProximo());
                    atual.setProximo(novoNo);
                }
            }
            tamanho++;
        }
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        Lista lista = new Lista();
        
        System.out.println("Digite o numero do caso teste");
        System.out.println("Caso 1 lista vazia");
        System.out.println("Caso 2 lista tamanho = 10, lista = {1,2,3,4,5,6,7,8,9,10}");
        
        int n = scanner.nextInt();
        while (n != 1 && n != 2) {
            System.out.println("Numero invalido, tente novamente");
            n = scanner.nextInt();
        }
        
        switch (n) {
            case 1:
                lista.imprimirLista();
                break;
            case 2:
                int[] elementos = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
                for (int i = 0; i < elementos.length; i++) {
                    lista.inserirElementosNaLista(i, elementos[i]);
                }
                lista.tamanho = 10;
                lista.imprimirLista();
                break;
            default:
                break;
        }
        System.out.println("A lista esta vazia?  " + lista.listaVazia());
        System.out.println("A lista tem um tamanho de: " + lista.tamanho);
        
        System.out.println("Digite a posicao do elemento da lista que deseja obter o valor.");
        int p = scanner.nextInt();
        int valorDoElementoBuscado = lista.posiçãoDeElemento(p);
        if (valorDoElementoBuscado != -1){
            System.out.println("O valor do elemento na posicao " + p + " é " + valorDoElementoBuscado);
        }
        
        
        System.out.println("Digite a posicao do elemento da lista que deseja modificar. ");
        p = scanner.nextInt();
        System.out.println("Digite o novo valor para o elemento que deseja modificar.");
        int novoValor = scanner.nextInt();
        int valorModificado = lista.modificarValorDeElemento(p, novoValor);
        if (valorModificado != -1) {
            System.out.println("Novo valor: " + valorModificado + " na posicao: " + p);
            lista.imprimirLista();
        }
        
        System.out.println("Digite a posicao do elemento da lista que deseja inserir.");
        p = scanner.nextInt();
        System.out.println("Digite um valor para o elemento que deseja inserir.");
        int valorNovoElemento = scanner.nextInt();
        int novoElemento = lista.inserirNaLista(p, valorNovoElemento);
        if (novoElemento != -1) {
            System.out.println("O novo elemento na posicao: " + p + " tem um valor de: " + valorNovoElemento);
            lista.imprimirLista();
            System.out.println("A lista tem um novo tamanho de: " + lista.tamanho);
        }
        
        System.out.println("Digite a posicao do elemento da lista que deseja remover.");
        p = scanner.nextInt();
        int valorDoElementoRemovido = lista.removerNaLista(p);
        if (valorDoElementoRemovido != -1) {
            System.out.println("O elemento na posicao: " + p + " foi removido com sucesso.");
            lista.imprimirLista();
            System.out.println("A lista tem um novo tamanho de: " + lista.tamanho);
        }
    }
}
