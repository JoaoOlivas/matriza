import java.util.Scanner;

public class VetorAnalise {

    // Função para verificar se um número é primo
    public static boolean isPrime(int num) {
        if (num <= 1) return false;
        for (int i = 2; i <= Math.sqrt(num); i++) {
            if (num % i == 0) return false;
        }
        return true;
    }

    // Função para verificar se um número é perfeito
    public static boolean isPerfect(int num) {
        int sum = 0;
        for (int i = 1; i <= num / 2; i++) {
            if (num % i == 0) {
                sum += i;
            }
        }
        return sum == num;
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        
        // Ler a quantidade de valores do vetor
        int n;
        do {
            System.out.print("Digite a quantidade de valores (1 a 9): ");
            n = scanner.nextInt();
        } while (n < 1 || n > 9);
        
        int[] vetor = new int[n];
        
        // Ler os valores do vetor garantindo que sejam maiores que zero
        for (int i = 0; i < n; i++) {
            do {
                System.out.print("Digite um número natural maior que zero para a posição " + (i + 1) + ": ");
                vetor[i] = scanner.nextInt();
            } while (vetor[i] <= 0);
        }

        // Inicialização de contadores e acumuladores
        int countPar = 0, countImpar = 0;
        int countDiv7 = 0;
        int countPrimo = 0;
        int countPerfeito = 0;
        int somaPosImpar = 0;
        long produtoIndiceImpar = 1; // Use long to handle potentially large products
        int somaPar = 0, countParTotal = 0;
        int somaImpar = 0, countImparTotal = 0;

        // Processamento dos valores do vetor
        for (int i = 0; i < n; i++) {
            if (vetor[i] % 2 == 0) {
                countPar++;
                somaPar += vetor[i];
                countParTotal++;
            } else {
                countImpar++;
                somaImpar += vetor[i];
                countImparTotal++;
            }

            if (vetor[i] % 7 == 0) {
                countDiv7++;
            }

            if (isPrime(vetor[i])) {
                countPrimo++;
            }

            if (isPerfect(vetor[i])) {
                countPerfeito++;
            }

            if (i % 2 != 0) {
                somaPosImpar += vetor[i];
                produtoIndiceImpar *= vetor[i];
            }
        }

        // Cálculo das médias
        double mediaPar = (countParTotal > 0) ? (double) somaPar / countParTotal : 0;
        double mediaImpar = (countImparTotal > 0) ? (double) somaImpar / countImparTotal : 0;

        // Impressão dos resultados
        System.out.println("Vetor: ");
        for (int num : vetor) {
            System.out.print(num + " ");
        }
        System.out.println();
        System.out.println("Quantidade de números pares: " + countPar);
        System.out.println("Quantidade de números ímpares: " + countImpar);
        System.out.println("Quantidade de números divisíveis por 7: " + countDiv7);
        System.out.println("Quantidade de números primos: " + countPrimo);
        System.out.println("Quantidade de números perfeitos: " + countPerfeito);
        System.out.println("Soma dos números nas posições ímpares: " + somaPosImpar);
        System.out.println("Produto dos números nos índices ímpares: " + produtoIndiceImpar);
        System.out.println("Média dos números pares: " + mediaPar);
        System.out.println("Média dos números ímpares: " + mediaImpar);
        System.out.println("A média dos números pares é " + 
                            (mediaPar > mediaImpar ? "maior" : (mediaPar < mediaImpar ? "menor" : "igual")) + 
                            " que a média dos números ímpares.");
        
        scanner.close();
    }
}
