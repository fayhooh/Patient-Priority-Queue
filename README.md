# Patient-Priority-Queue
import java.util.PriorityQueue;
import java.util.Comparator;

class Patient {
    String name;
    int priority;
    int arrivalOrder;

    Patient(String name, int priority, int arrivalOrder) {
        this.name = name;
        this.priority = priority;
        this.arrivalOrder = arrivalOrder;
    }
}

public class PatientPriorityQueue {

    static int count = 0;

    static PriorityQueue<Patient> patients =
        new PriorityQueue<>(
            Comparator.comparingInt((Patient p) -> p.priority)
                      .thenComparingInt(p -> p.arrivalOrder)
        );

    // Add a patient
    public static void addPatient(String name, int priority) {

        if (priority < 1 || priority > 3) {
            System.out.println("Invalid priority!");
            return;
        }

        patients.add(new Patient(name, priority, count++));

        System.out.println(name + " added successfully.");
    }

    // Treat the next patient
    public static void treatNextPatient() {

        if (patients.isEmpty()) {
            System.out.println("No patients waiting.");
            return;
        }

        Patient p = patients.poll();

        System.out.println("Treating: " + p.name +
                           " | Priority: " + p.priority);
    }

    public static void main(String[] args) {

        System.out.println("PATIENT PRIORITY QUEUE SYSTEM");

        // Add six patients
        addPatient("P1", 3);
        addPatient("P2", 1);
        addPatient("P3", 2);
        addPatient("P4", 1);
        addPatient("P5", 3);
        addPatient("P6", 2);

        System.out.println("\nFirst three patients:");

        // Treat three patients
        treatNextPatient();
        treatNextPatient();
        treatNextPatient();

        // Add a new emergency patient
        System.out.println("\nAdding new emergency patient:");

        addPatient("P7", 1);

        System.out.println("\nRemaining patients:");

        // Treat everyone remaining
        while (!patients.isEmpty()) {
            treatNextPatient();
        }

        System.out.println("\nAll patients treatedf\.");
    }
}
