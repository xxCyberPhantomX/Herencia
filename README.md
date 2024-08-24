# Herencia
// Interfaz para estrategia de cálculo de precio
interface EstrategiaPrecio {
    double calcularPrecio();
}

// Implementación para cálculo de precio por peso
class PrecioPorPeso implements EstrategiaPrecio {
    private double precioPorKilo;
    private double peso;

    public PrecioPorPeso(double precioPorKilo, double peso) {
        this.precioPorKilo = precioPorKilo;
        this.peso = peso;
    }

    @Override
    public double calcularPrecio() {
        return precioPorKilo * peso;
    }
}

// Implementación para cálculo de precio por volumen
class PrecioPorVolumen implements EstrategiaPrecio {
    private double precioPorLitro;
    private double volumen;

    public PrecioPorVolumen(double precioPorLitro, double volumen) {
        this.precioPorLitro = precioPorLitro;
        this.volumen = volumen;
    }

    @Override
    public double calcularPrecio() {
        return precioPorLitro * volumen;
    }
}

// Clase Producto que utiliza composición
class Producto {
    private String nombre;
    private EstrategiaPrecio estrategiaPrecio;

    public Producto(String nombre, EstrategiaPrecio estrategiaPrecio) {
        this.nombre = nombre;
        this.estrategiaPrecio = estrategiaPrecio;
    }

    public double calcularPrecio() {
        return estrategiaPrecio.calcularPrecio();
    }
}

// Ejemplo de uso
public class Supermercado {
    public static void main(String[] args) {
        EstrategiaPrecio precioManzana = new PrecioPorPeso(2.5, 1.2);  // 2.5 por kilo, 1.2 kilos
        EstrategiaPrecio precioLeche = new PrecioPorVolumen(1.5, 2);   // 1.5 por litro, 2 litros

        Producto manzana = new Producto("Manzana", precioManzana);
        Producto leche = new Producto("Leche", precioLeche);

        System.out.println(manzana.calcularPrecio());  // Output: 3.0
        System.out.println(leche.calcularPrecio());    // Output: 3.0
    }
}
