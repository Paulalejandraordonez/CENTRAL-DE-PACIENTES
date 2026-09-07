# CENTRAL-DE-PACIENTES
CentralDePacientes/
│
├── src/
│   ├── Main.java
│   ├── Paciente.java
│   ├── Nodo.java
│   └── ListaPacientes.java
│
├── docs/
│   └── README.md
│
└── README.md
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
                id, nombre, edad, diagnostico  /**
 * Representa un nodo de una lista simplemente enlazada.
 *
 * Cada nodo contiene un paciente y una referencia
 * al siguiente nodo de la lista.
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
}  /**
 * Administra una lista simplemente enlazada de pacientes.
 */
public class ListaPacientes {

    private Nodo cabeza;

    /**
     * Inicializa una lista vacía.
     */
    public ListaPacientes() {
        cabeza = null;
    }

    /**
     * Inserta un paciente al final de la lista.
     *
     * @param paciente paciente que será agregado.
     */
    public void insertar(Paciente paciente) {

        Nodo nuevo = new Nodo(paciente);

        // Si la lista está vacía,
        // el nuevo nodo se convierte en la cabeza.
        if (cabeza == null) {
            cabeza = nuevo;
            return;
        }

        // Se recorre la lista hasta encontrar
        // el último nodo.
        Nodo actual = cabeza;

        while (actual.getSiguiente() != null) {
            actual = actual.getSiguiente();
        }

        // Se enlaza el último nodo con el nuevo.
        actual.setSiguiente(nuevo);
    }

    /**
     * Muestra todos los pacientes registrados.
     */
    public void mostrarPacientes() {

        if (cabeza == null) {
            System.out.println("No hay pacientes registrados.");
            return;
        }

        Nodo actual = cabeza;

        while (actual != null) {
            System.out.println(actual.getPaciente());
            actual = actual.getSiguiente();
        }
    }

    /**
     * Busca un paciente utilizando su identificador.
     *
     * @param id identificador del paciente.
     * @return paciente encontrado o null si no existe.
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
     * Elimina un paciente utilizando su identificador.
     *
     * @param id identificador del paciente.
     * @return true si fue eliminado, false si no fue encontrado.
     */
    public boolean eliminar(int id) {

        // Si la lista está vacía.
        if (cabeza == null) {
            return false;
        }

        // Si el paciente se encuentra en el primer nodo.
        if (cabeza.getPaciente().getId() == id) {
            cabeza = cabeza.getSiguiente();
            return true;
        }

        Nodo actual = cabeza;

        // Se busca el nodo anterior al que se quiere eliminar.
        while (actual.getSiguiente() != null) {

            if (actual.getSiguiente()
                    .getPaciente()
                    .getId() == id) {

                actual.setSiguiente(
                        actual.getSiguiente().getSiguiente()
                );

                return true;
            }

            actual = actual.getSiguiente();
        }

        return false;
    }

    /**
     * Verifica si la lista se encuentra vacía.
     *
     * @return true si está vacía.
     */
    public boolean estaVacia() {
        return cabeza == null;
    }
}/**
 * Clase principal del proyecto Central de Pacientes.
 */
public class Main {

    public static void main(String[] args) {

        // Se crea la lista de pacientes.
        ListaPacientes lista = new ListaPacientes();

        // ==========================================
        // REGISTRO DE PACIENTES
        // ==========================================

        lista.insertar(
                new Paciente(
                        1,
                        "Ana Rodríguez",
                        25,
                        "Dolor de cabeza"
                )
        );

        lista.insertar(
                new Paciente(
                        2,
                        "Carlos Gómez",
                        42,
                        "Hipertensión"
                )
        );

        lista.insertar(
                new Paciente(
                        3,
                        "Laura Martínez",
                        31,
                        "Gastritis"
                )
        );

        // ==========================================
        // MOSTRAR PACIENTES
        // ==========================================

        System.out.println("==========================================");
        System.out.println("          CENTRAL DE PACIENTES");
        System.out.println("==========================================");

        System.out.println("\nPACIENTES REGISTRADOS:");
        lista.mostrarPacientes();

        // ==========================================
        // BÚSQUEDA
        // ==========================================

        System.out.println("\n==========================================");
        System.out.println("BUSQUEDA DE PACIENTE");
        System.out.println("==========================================");

        int idBuscar = 2;

        Paciente encontrado = lista.buscarPorId(idBuscar);

        if (encontrado != null) {
            System.out.println("Paciente encontrado:");
            System.out.println(encontrado);
        } else {
            System.out.println(
                    "No se encontró un paciente con ID: "
                            + idBuscar
            );
        }

        // ==========================================
        // ELIMINACIÓN
        // ==========================================

        System.out.println("\n==========================================");
        System.out.println("ELIMINACION DE PACIENTE");
        System.out.println("==========================================");

        int idEliminar = 2;

        boolean eliminado = lista.eliminar(idEliminar);

        if (eliminado) {
            System.out.println(
                    "El paciente con ID "
                            + idEliminar
                            + " fue eliminado correctamente."
            );
        } else {
            System.out.println(
                    "No se encontró el paciente con ID "
                            + idEliminar
            );
        }

        // ==========================================
        // LISTA ACTUALIZADA
        // ==========================================

        System.out.println("\n==========================================");
        System.out.println("LISTA ACTUALIZADA");
        System.out.println("==========================================");

        lista.mostrarPacientes();
    }
}
        );
    }
