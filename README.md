import java.util.ArrayList;
import java.util.List;
import java.util.Scanner;

public class PatientApp {

    static List<Appointment> appointments = new ArrayList<>();
    static int nextAppointmentId = 1;

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.println("Добро пожаловать в приложение для пациентов!");

        while (true) {
            System.out.println("\nВыберите действие:");
            System.out.println("1. Записаться на прием");
            System.out.println("2. Отменить запись");
            System.out.println("3. Просмотреть записи");
            System.out.println("4. Выйти");

            int choice = scanner.nextInt();
            scanner.nextLine(); // Consume newline

            switch (choice) {
                case 1:
                    System.out.println("Введите имя врача:");
                    String doctorName = scanner.nextLine();
                    System.out.println("Введите дату приема (ДД.ММ.ГГГГ):");
                    String appointmentDate = scanner.nextLine();
                    createAppointment(doctorName, appointmentDate);
                    System.out.println("Запись на прием к " + doctorName + " на " + appointmentDate + " успешно создана!");
                    break;
                case 2:
                    System.out.println("Введите номер записи для отмены:");
                    int appointmentId = scanner.nextInt();
                    scanner.nextLine(); // Consume newline
                    cancelAppointment(appointmentId);
                    break;
                case 3:
                    viewAppointments();
                    break;
                case 4:
                    System.out.println("До свидания!");
                    System.exit(0);
                default:
                    System.out.println("Неверный выбор. Пожалуйста, попробуйте снова.");
            }
        }
    }

    static void createAppointment(String doctorName, String appointmentDate) {
        Appointment appointment = new Appointment(nextAppointmentId, doctorName, appointmentDate);
        appointments.add(appointment);
        nextAppointmentId++;
    }

    static void cancelAppointment(int appointmentId) {
        for (int i = 0; i < appointments.size(); i++) {
            if (appointments.get(i).getId() == appointmentId) {
                appointments.remove(i);
                System.out.println("Запись с номером " + appointmentId + " успешно отменена!");
                return;
            }
        }
        System.out.println("Запись с номером " + appointmentId + " не найдена.");
    }

    static void viewAppointments() {
        if (appointments.isEmpty()) {
            System.out.println("У вас нет записей.");
            return;
        }
        System.out.println("Список ваших записей:");
        for (Appointment appointment : appointments) {
            System.out.println("Номер: " + appointment.getId() + ", Врач: " + appointment.getDoctorName() + ", Дата: " + appointment.getAppointmentDate());
        }
    }
}

class Appointment {
    private int id;
    private String doctorName;
    private String appointmentDate;

    Appointment(int id, String doctorName, String appointmentDate) {
        this.id = id;
        this.doctorName = doctorName;
        this.appointmentDate = appointmentDate;
    }

    int getId() {
        return id;
    }

    String getDoctorName() {
        return doctorName;
    }

    String getAppointmentDate() {
        return appointmentDate;
    }
}
