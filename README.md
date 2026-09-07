# CENTRAL-DE-PACIENTES
Central de Pacientes

El proyecto fue desarrollado utilizando el lenguaje de programación Java y aplicando los principios de programación orientada a objetos.

La estructura principal utilizada es una lista simplemente enlazada, conformada por nodos.

Cada nodo contiene la información de un paciente y una referencia al siguiente nodo.

Decisiones de implementación

Se decidió separar el proyecto en diferentes clases con el objetivo de mantener una organización clara y facilitar el mantenimiento del código.

La clase Paciente se utiliza exclusivamente para representar los datos del paciente.

La clase Nodo permite construir la estructura enlazada.

La clase ListaPacientes concentra las operaciones relacionadas con la estructura de datos.

Finalmente, la clase Main permite ejecutar y comprobar el funcionamiento de la aplicación.

Estructura de datos

La estructura utilizada es una lista simplemente enlazada.

Cada nodo mantiene una referencia hacia el siguiente elemento de la lista. El último nodo tiene como referencia null, indicando el final de la estructura.

Operaciones

Las principales operaciones desarrolladas son:

Insertar un paciente.
Mostrar todos los pacientes.
Buscar un paciente por ID.
Eliminar un paciente por ID.
Verificar si la lista está vacía.
Conclusión

La implementación permite demostrar de manera práctica el funcionamiento de una lista simplemente enlazada y las operaciones fundamentales de inserción, búsqueda, recorrido y eliminación de nodos.

La separación de responsabilidades entre las clases permite mantener un código organizado y facilita la comprensión de la solución.
/**
 * Representa la información básica de un paciente.
 */
public class Paciente {

    private final int id;
    private final String nombre;
    private final int edad;
    private final String diagnostico;

    /**
     * Constructor de la clase Paciente.
     *
     * @param id identificador único del paciente
     * @param nombre nombre completo del paciente
     * @param edad edad del paciente
     * @param diagnostico diagnóstico del paciente
     */
    public Paciente(int id, String nombre, int edad, String diagnostico) {
        this.id = id;
        this.nombre = nombre;
        this.edad = edad;
        this.diagnostico = diagnostico;
    }

    public int getId() {
        return id;
    }

    public String getNombre() {
        return nombre;
    }

    public int getEdad() {
        return edad;
    }

    public String getDiagnostico() {
        return diagnostico;
    }

    /**
     * Permite mostrar la información del paciente
     * de una manera organizada.
     */
    @Override
    public String toString() {
        return String.format(
                "ID: %d | Nombre: %s | Edad: %d | Diagnóstico: %s",
                id,
                nombre,
                edad,
                diagnostico
        );
    }
}
/**
 * Nodo de la lista simplemente enlazada.
 * Cada nodo guarda un paciente y la referencia al siguiente nodo.
 */
public class Nodo {
    private Paciente paciente;
    private Nodo siguiente;

    public Nodo(Paciente paciente) {
        this.paciente = paciente;
        this.siguiente = null;
    }

    public Paciente getPaciente() {
        return paciente;
    }

    public void setPaciente(Paciente paciente) {
        this.paciente = paciente;
    }

    public Nodo getSiguiente() {
        return siguiente;
    }

    public void setSiguiente(Nodo siguiente) {
        this.siguiente = siguiente;
    }
}/**
 * Lista simplemente enlazada para almacenar pacientes.
 *
 * No utiliza ArrayList, LinkedList ni ninguna otra colección de Java.
 */
public class ListaPacientes {
    private Nodo cabeza;
    private int tamanio;

    public ListaPacientes() {
        cabeza = null;
        tamanio = 0;
    }

    public boolean estaVacia() {
        return cabeza == null;
    }

    public int getTamanio() {
        return tamanio;
    }

    /**
     * Inserta un paciente al final de la lista recorriendo los nodos.
     */
    public void insertarAlFinal(Paciente paciente) {
        Nodo nuevoNodo = new Nodo(paciente);

        if (estaVacia()) {
            cabeza = nuevoNodo;
        } else {
            Nodo actual = cabeza;

            while (actual.getSiguiente() != null) {
                actual = actual.getSiguiente();
            }

            actual.setSiguiente(nuevoNodo);
        }

        tamanio++;
    }

    /**
     * Busca un paciente por su identificador.
     *
     * @return el paciente encontrado o null si no existe
     */
    public Paciente buscarPorId(int id) {
        Nodo actual = cabeza;

        while (actual != null) {
            if (actual.getPaciente().getId() == id) {
                return actual.getPaciente();
            }

            actual = actual.getSiguiente();
        }

        return null;
    }

    /**
     * Elimina el primer paciente que tenga el identificador indicado.
     *
     * @return true si se eliminó; false si no se encontró
     */
    public boolean eliminarPorId(int id) {
        if (estaVacia()) {
            return false;
        }

        // Eliminar el primer nodo
        if (cabeza.getPaciente().getId() == id) {
            cabeza = cabeza.getSiguiente();
            tamanio--;
            return true;
        }

        Nodo anterior = cabeza;
        Nodo actual = cabeza.getSiguiente();

        while (actual != null) {
            if (actual.getPaciente().getId() == id) {
                anterior.setSiguiente(actual.getSiguiente());
                tamanio--;
                return true;
            }

            anterior = actual;
            actual = actual.getSiguiente();
        }

        return false;
    }

    /**
     * Recorre la lista desde la cabeza hasta el último nodo
     * y muestra la información de cada paciente.
     */
    public void mostrarTodos() {
        if (estaVacia()) {
            System.out.println("No hay pacientes registrados.");
            return;
        }

        Nodo actual = cabeza;
        int posicion = 1;

        while (actual != null) {
            System.out.println(posicion + ". " + actual.getPaciente());
            actual = actual.getSiguiente();
            posicion++;
        }
    }
}A continuación tienes el código completo. Guarda cada bloque en un archivo separado dentro de:

```text
CentralDePacientes/src/
```

También puedes descargarlo aquí:

**[Descargar CentralDePacientes.zip](sandbox:/CentralDePacientes.zip)**

---

## 1. `Paciente.java`

```java
/**
 * Representa la información básica de un paciente.
 */
public class Paciente {
    private final int id;
    private final String nombre;
    private final int edad;
    private final String diagnostico;

    public Paciente(int id, String nombre, int edad, String diagnostico) {
        this.id = id;
        this.nombre = nombre;
        this.edad = edad;
        this.diagnostico = diagnostico;
    }

    public int getId() {
        return id;
    }

    public String getNombre() {
        return nombre;
    }

    public int getEdad() {
        return edad;
    }

    public String getDiagnostico() {
        return diagnostico;
    }

    @Override
    public String toString() {
        return String.format(
                "ID: %d | Nombre: %s | Edad: %d | Diagnóstico: %s",
                id, nombre, edad, diagnostico
        );
    }
}
```

---

## 2. `Nodo.java`

```java
/**
 * Nodo de la lista simplemente enlazada.
 * Cada nodo guarda un paciente y la referencia al siguiente nodo.
 */
public class Nodo {
    private Paciente paciente;
    private Nodo siguiente;

    public Nodo(Paciente paciente) {
        this.paciente = paciente;
        this.siguiente = null;
    }

    public Paciente getPaciente() {
        return paciente;
    }

    public void setPaciente(Paciente paciente) {
        this.paciente = paciente;
    }

    public Nodo getSiguiente() {
        return siguiente;
    }

    public void setSiguiente(Nodo siguiente) {
        this.siguiente = siguiente;
    }
}
```

---

## 3. `ListaPacientes.java`

```java
/**
 * Lista simplemente enlazada para almacenar pacientes.
 *
 * No utiliza ArrayList, LinkedList ni ninguna otra colección de Java.
 */
public class ListaPacientes {
    private Nodo cabeza;
    private int tamanio;

    public ListaPacientes() {
        cabeza = null;
        tamanio = 0;
    }

    public boolean estaVacia() {
        return cabeza == null;
    }

    public int getTamanio() {
        return tamanio;
    }

    /**
     * Inserta un paciente al final de la lista recorriendo los nodos.
     */
    public void insertarAlFinal(Paciente paciente) {
        Nodo nuevoNodo = new Nodo(paciente);

        if (estaVacia()) {
            cabeza = nuevoNodo;
        } else {
            Nodo actual = cabeza;

            while (actual.getSiguiente() != null) {
                actual = actual.getSiguiente();
            }

            actual.setSiguiente(nuevoNodo);
        }

        tamanio++;
    }

    /**
     * Busca un paciente por su identificador.
     *
     * @return el paciente encontrado o null si no existe
     */
    public Paciente buscarPorId(int id) {
        Nodo actual = cabeza;

        while (actual != null) {
            if (actual.getPaciente().getId() == id) {
                return actual.getPaciente();
            }

            actual = actual.getSiguiente();
        }

        return null;
    }

    /**
     * Elimina el primer paciente que tenga el identificador indicado.
     *
     * @return true si se eliminó; false si no se encontró
     */
    public boolean eliminarPorId(int id) {
        if (estaVacia()) {
            return false;
        }

        // Eliminar el primer nodo
        if (cabeza.getPaciente().getId() == id) {
            cabeza = cabeza.getSiguiente();
            tamanio--;
            return true;
        }

        Nodo anterior = cabeza;
        Nodo actual = cabeza.getSiguiente();

        while (actual != null) {
            if (actual.getPaciente().getId() == id) {
                anterior.setSiguiente(actual.getSiguiente());
                tamanio--;
                return true;
            }

            anterior = actual;
            actual = actual.getSiguiente();
        }

        return false;
    }

    /**
     * Recorre la lista desde la cabeza hasta el último nodo
     * y muestra la información de cada paciente.
     */
    public void mostrarTodos() {
        if (estaVacia()) {
            System.out.println("No hay pacientes registrados.");
            return;
        }

        Nodo actual = cabeza;
        int posicion = 1;

        while (actual != null) {
            System.out.println(posicion + ". " + actual.getPaciente());
            actual = actual.getSiguiente();
            posicion++;
        }
    }
}
```

---

## 4. `Main.java`

```java
import java.util.Scanner;

/**
 * Punto de entrada de la aplicación CentralDePacientes.
 */
public class Main {
    private static final int EDAD_MINIMA = 0;
    private static final int EDAD_MAXIMA = 120;

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        ListaPacientes listaPacientes = new ListaPacientes();
        boolean continuar = true;

        System.out.println("====================================");
        System.out.println("       CENTRAL DE PACIENTES");
        System.out.println("====================================");

        while (continuar) {
            mostrarMenu();

            int opcion = leerEntero(
                    scanner,
                    "Seleccione una opción: "
            );

            switch (opcion) {
                case 1:
                    registrarPaciente(scanner, listaPacientes);
                    break;

                case 2:
                    mostrarPacientes(listaPacientes);
                    break;

                case 3:
                    buscarPaciente(scanner, listaPacientes);
                    break;

                case 4:
                    eliminarPaciente(scanner, listaPacientes);
                    break;

                case 5:
                    System.out.println(
                            "\nCantidad de pacientes registrados: "
                                    + listaPacientes.getTamanio()
                    );
                    break;

                case 0:
                    continuar = false;
                    System.out.println(
                            "\nPrograma finalizado. Hasta pronto."
                    );
                    break;

                default:
                    System.out.println(
                            "\nOpción inválida. "
                                    + "Seleccione un número del 0 al 5."
                    );
            }
        }

        scanner.close();
    }

    private static void mostrarMenu() {
        System.out.println("\n--------------- MENÚ ---------------");
        System.out.println("1. Registrar paciente");
        System.out.println("2. Mostrar todos los pacientes");
        System.out.println("3. Buscar paciente por ID");
        System.out.println("4. Eliminar paciente por ID");
        System.out.println("5. Mostrar cantidad de pacientes");
        System.out.println("0. Salir");
        System.out.println("------------------------------------");
    }

    private static void registrarPaciente(
            Scanner scanner,
            ListaPacientes listaPacientes
    ) {
        System.out.println("\n--- Registro de paciente ---");

        int id = leerEnteroPositivo(
                scanner,
                "ID del paciente: "
        );

        if (listaPacientes.buscarPorId(id) != null) {
            System.out.println("Ya existe un paciente con ese ID.");
            return;
        }

        String nombre = leerTextoNoVacio(
                scanner,
                "Nombre completo: "
        );

        int edad = leerEdad(scanner);

        String diagnostico = leerTextoNoVacio(
                scanner,
                "Diagnóstico: "
        );

        Paciente paciente = new Paciente(
                id,
                nombre,
                edad,
                diagnostico
        );

        listaPacientes.insertarAlFinal(paciente);

        System.out.println(
                "Paciente registrado correctamente."
        );
    }

    private static void mostrarPacientes(
            ListaPacientes listaPacientes
    ) {
        System.out.println("\n--- Lista de pacientes ---");
        listaPacientes.mostrarTodos();
    }

    private static void buscarPaciente(
            Scanner scanner,
            ListaPacientes listaPacientes
    ) {
        System.out.println("\n--- Búsqueda de paciente ---");

        int id = leerEnteroPositivo(
                scanner,
                "Ingrese el ID a buscar: "
        );

        Paciente paciente = listaPacientes.buscarPorId(id);

        if (paciente == null) {
            System.out.println(
                    "No se encontró un paciente con ese ID."
            );
        } else {
            System.out.println("Paciente encontrado:");
            System.out.println(paciente);
        }
    }

    private static void eliminarPaciente(
            Scanner scanner,
            ListaPacientes listaPacientes
    ) {
        System.out.println("\n--- Eliminación de paciente ---");

        int id = leerEnteroPositivo(
                scanner,
                "Ingrese el ID a eliminar: "
        );

        if (listaPacientes.eliminarPorId(id)) {
            System.out.println(
                    "Paciente eliminado correctamente."
            );
        } else {
            System.out.println(
                    "No se encontró un paciente con ese ID."
            );
        }
    }

    private static int leerEdad(Scanner scanner) {
        while (true) {
            int edad = leerEntero(
                    scanner,
                    "Edad (0-120): "
            );

            if (edad >= EDAD_MINIMA && edad <= EDAD_MAXIMA) {
                return edad;
            }

            System.out.println(
                    "La edad debe estar entre 0 y 120 años."
            );
        }
    }

    private static int leerEnteroPositivo(
            Scanner scanner,
            String mensaje
    ) {
        while (true) {
            int valor = leerEntero(scanner, mensaje);

            if (valor > 0) {
                return valor;
            }

            System.out.println(
                    "El valor debe ser un número entero positivo."
            );
        }
    }

    /**
     * Lee un entero usando una línea completa
     * para evitar errores de Scanner.
     */
    private static int leerEntero(
            Scanner scanner,
            String mensaje
    ) {
        while (true) {
            System.out.print(mensaje);

            String entrada = scanner.nextLine().trim();

            try {
                return Integer.parseInt(entrada);
            } catch (NumberFormatException exception) {
                System.out.println(
                        "Entrada inválida. "
                                + "Escriba un número entero."
                );
            }
        }
    }

    private static String leerTextoNoVacio(
            Scanner scanner,
            String mensaje
    ) {
        while (true) {
            System.out.print(mensaje);

            String texto = scanner.nextLine().trim();

            if (!texto.isEmpty()) {
                return texto;
            }

            System.out.println(
                    "Este campo no puede quedar vacío."
            );
        }
    }
}
```

## Compilar y ejecutar

Desde la carpeta `CentralDePacientes`:

```bash
mkdir -p out
javac -encoding UTF-8 -d out src/*.java
java -cp out Main
