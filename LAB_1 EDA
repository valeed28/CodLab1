package Laboratorio_EDA_1;
import java.util.Scanner;

public class BigVigenere {

    private int[] key;
    private char[][] alphabet;
    private final int alphabet_size = 64;
    private final String character = "abcdefghijklmnñopqrstuvwxyzABCDEFGHIJKLMNÑOPQRSTUVWXYZ0123456789";

    public BigVigenere() {
        Scanner entrada = new Scanner(System.in);
        String claveKey = entrada.nextLine();
        this.key = convertirClave(claveKey);
        this.alphabet = generarMatrizAlphabet();
        entrada.close(); }

    public BigVigenere(String numericKey) {
        this.key = convertirClave(numericKey);
        this.alphabet = generarMatrizAlphabet(); }

    private int[] convertirClave(String claveKey) {
        try {
            String[] partesClave = claveKey.split(" ");
            int[] arreglo = new int[partesClave.length];
            for (int i = 0; i < partesClave.length; i++) {
                arreglo[i] = Integer.parseInt(partesClave[i]) % alphabet_size; }
            return arreglo; }
            catch (NumberFormatException e) {
            throw new IllegalArgumentException("Clave invalida,revise que solo haya ingresado numeros separados por espacios."); }
    }

    private char[][] generarMatrizAlphabet() {
        char[][] matriz = new char[alphabet_size][alphabet_size];
        for (int fila = 0; fila < alphabet_size; fila++) {
            for (int col = 0; col < alphabet_size; col++) {
                matriz[fila][col] = character.charAt((fila + col) % alphabet_size);}
        } return matriz; }

    public String encrypt(String message) {
        StringBuilder resultado = new StringBuilder();
        for (int i = 0; i < message.length(); i++) {
            char caracterActual = message.charAt(i);
            int fila = character.indexOf(caracterActual);
            if (fila == -1) {
                throw new IllegalArgumentException("El mensaje contiene caracteres no soportados: " + caracterActual); }
            int col = key[i % key.length];
            resultado.append(alphabet[fila][col]); }
        return resultado.toString(); }

    public String decrypt(String encryptedMessage) {
        StringBuilder original = new StringBuilder();
        for (int i = 0; i < encryptedMessage.length(); i++) {
            char caracterActual = encryptedMessage.charAt(i);
            int col = key[i % key.length];
            int fila = -1;

            for (int j = 0; j < alphabet_size; j++) {
                if (alphabet[j][col] == caracterActual) {
                    fila = j;
                    break;}
            }
            if (fila == -1) {
                throw new IllegalArgumentException("El mensaje contiene caracteres no soportados.");}
            original.append(character.charAt(fila));}
        return original.toString(); }

    public void reEncrypt() {
        Scanner entrada = new Scanner(System.in);
        System.out.println(" ");
        System.out.println("(Practica) Para decifrar:  ");
        System.out.print("Introduce el mensaje cifrado: ");
        String mensajeCifrado = entrada.nextLine();
        String descifrado = decrypt(mensajeCifrado);
        System.out.println("Mensaje descifrado: " + descifrado);
        System.out.print("Nueva clave (numeros separados por espacios): ");
        String nuevaClave = entrada.nextLine();

        try {
            this.key = convertirClave(nuevaClave);
            System.out.println("Clave guardada y cifrada correctamente.");
        } catch (IllegalArgumentException e) {
            System.out.println(e.getMessage());
            return; }

        String nuevoCifrado = encrypt(descifrado);
        System.out.println("Texto reencriptado: " + nuevoCifrado);
        entrada.close();}

    public char search(int position) {
        if (position < 0 || position >= alphabet_size * alphabet_size) {
            throw new IllegalArgumentException("Posicion fuera de rango.");}

        int contador = 0;
        for (int fila = 0; fila < alphabet_size; fila++) {
            for (int col = 0; col < alphabet_size; col++) {
                if (contador == position) {
                    return alphabet[fila][col];
                }contador++;
            }
        } throw new IllegalArgumentException("Posicion no encontrada.");
    }

    public char optimalSearch(int position) {
        if (position < 0 || position >= alphabet_size * alphabet_size) {
            throw new IllegalArgumentException("Posicion fuera de rango.");
        }

        int fila = position / alphabet_size;
        int col = position % alphabet_size;
        return alphabet[fila][col];
    }

    public static void main(String[] args) {
        try {
            BigVigenere vigenere = new BigVigenere("3 2 5 7");
            
            System.out.println("Ejemplo: ");
            String mensaje = "Laboratorio1Ñ";
            System.out.println("Mensaje original: " + mensaje);
            String mensajeCifrado = vigenere.encrypt(mensaje);
            System.out.println("Mensaje cifrado: " + mensajeCifrado);
            String mensajeDescifrado = vigenere.decrypt(mensajeCifrado);
            System.out.println("Mensaje descifrado: " + mensajeDescifrado);
            vigenere.reEncrypt();

        } catch (IllegalArgumentException e) {
            System.out.println("Error: " + e.getMessage());}
    }
}
