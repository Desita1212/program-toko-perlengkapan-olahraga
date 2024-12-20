# program-toko-perlengkapan-olahraga
import java.util.ArrayList;
import java.util.Scanner;

/**
 *
 * @author desita
 */
public class Tokoperalatanolahraga {

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        // Membuat daftar produk
        ArrayList<Product> productList = new ArrayList<>();
        productList.add(new Product("Tali skipping", 35000, 59));
        productList.add(new Product("Matras yoga", 45000, 100));
        productList.add(new Product("Sepeda statis", 1200000, 30));
        productList.add(new Product("Raket badminton", 95000, 25));

        // Keranjang belanja
        ArrayList<CartItem> cart = new ArrayList<>();

        int choice;
        boolean isRunning = true;

        while (isRunning) {
            // Menampilkan menu utama
            System.out.println("\n=== MENU UTAMA ===");
            System.out.println("1. Lihat Produk");
            System.out.println("2. Pilih Produk");
            System.out.println("3. Cek Stok Produk");
            System.out.println("4. Tambah ke Keranjang");
            System.out.println("5. Lihat Keranjang");
            System.out.println("6. Keluar");
            System.out.print("Masukkan pilihan Anda: ");
            choice = scanner.nextInt();

            switch (choice) {
                case 1 -> {
                    // Lihat semua produk
                    System.out.println("\n=== DAFTAR PRODUK ===");
                    for (int i = 0; i < productList.size(); i++) {
                        System.out.println((i + 1) + ". " + productList.get(i).getProductName());
                    }
                }

                case 2 -> {
                    // Pilih produk untuk melihat detail
                    System.out.println("\nPilih produk berdasarkan nomor:");
                    for (int i = 0; i < productList.size(); i++) {
                        System.out.println((i + 1) + " " + productList.get(i).getProductName());
                    }
                    System.out.print("Masukkan nomor produk: ");
                    int productChoice = scanner.nextInt();

                    if (productChoice >= 1 && productChoice <= productList.size()) {
                        Product selectedProduct = productList.get(productChoice - 1);
                        System.out.println("\nDetail Produk:");
                        System.out.println("Nama Produk: " + selectedProduct.getProductName());
                        selectedProduct.displayPrice();
                        System.out.println("Stok Tersisa: " + selectedProduct.getStock());
                    } else {
                        System.out.println("Pilihan tidak valid!");
                    }
                }

                case 3 -> {
                    // Cek stok produk
                    System.out.println("\nCek stok produk:");
                    for (int i = 0; i < productList.size(); i++) {
                        Product product = productList.get(i);
                        System.out.println((i + 1) + " " + product.getProductName() + " - Stok: " + product.getStock());
                    }
                }

                case 4 -> {
                    // Tambahkan produk ke keranjang belanja
                    System.out.println("\nPilih produk untuk ditambahkan ke keranjang:");
                    for (int i = 0; i < productList.size(); i++) {
                        System.out.println((i + 1) + " " + productList.get(i).getProductName());
                    }
                    System.out.print("Masukkan nomor produk: ");
                    int cartChoice = scanner.nextInt();

                    if (cartChoice >= 1 && cartChoice <= productList.size()) {
                        Product selectedProduct = productList.get(cartChoice - 1);

                        System.out.print("Masukkan jumlah yang ingin dibeli: ");
                        int quantity = scanner.nextInt();

                        if (quantity <= 0) {
                            System.out.println("Jumlah harus lebih dari 0.");
                        } else if (quantity > selectedProduct.getStock()) {
                            System.out.println("Stok tidak mencukupi!");
                        } else {
                            selectedProduct.sellProduct(quantity);
                            cart.add(new CartItem(selectedProduct.getProductName(), selectedProduct.getPrice(), quantity));
                            System.out.println(quantity + " " + selectedProduct.getProductName() + " berhasil ditambahkan ke keranjang.");
                        }
                    } else {
                        System.out.println("Pilihan tidak valid!");
                    }
                }

                case 5 -> {
                    // Lihat isi keranjang
                    System.out.println("\n=== KERANJANG BELANJA ===");
                    if (cart.isEmpty()) {
                        System.out.println("Keranjang belanja kosong.");
                    } else {
                        double total = 0;
                        for (CartItem item : cart) {
                            System.out.println("- " + item.getProductName() + " | Jumlah: " + item.getQuantity() + " | Harga: Rp" + (item.getPrice() * item.getQuantity()));
                            total += item.getPrice() * item.getQuantity();
                        }
                        System.out.println("Total Belanja: Rp" + total);
                    }
                }

                case 6 -> {
                    // Keluar dari program
                    System.out.println("Terima kasih telah berbelanja. Sampai jumpa!");
                    isRunning = false;
                }

                default -> System.out.println("Pilihan tidak valid! Silakan coba lagi.");
            }
        }

        scanner.close();
    }
}

package com.mycompany.tokoperalatanolahraga;

/**
 *
 * @author desita
 */
class Product {
    private String productName;
    private double price;
    private int stock;

    public Product(String productName, double price, int stock) {
        this.productName = productName;
        this.price = price;
        this.stock = stock;
    }

    public String getProductName() {
        return productName;
    }

    public double getPrice() {
        return price;
    }

    public int getStock() {
        return stock;
    }

    public void sellProduct(int quantity) {
        stock -= quantity;
    }

    public void displayPrice() {
        System.out.println("Harga: Rp" + price);
    }
}


package com.mycompany.tokoperalatanolahraga;

/**
 *
 * @author desita
 */
class CartItem {
    private String productName;
    private double price;
    private int quantity;

    public CartItem(String productName, double price, int quantity) {
        this.productName = productName;
        this.price = price;
        this.quantity = quantity;
    }

    public String getProductName() {
        return productName;
    }

    public double getPrice() {
        return price;
    }

    public int getQuantity() {
        return quantity;
    }
}
