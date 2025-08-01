# Пустой репозиторий для работы с Java кодом в Android Studio

import java.util.Scanner;

public class Main {
public static void main(String[] args) {

        Scanner scanner = new Scanner(System.in);
        Drive drive = new Drive();
        Auto[] autos = new Auto[3];

        for (int i = 0; i < 3; i++) {

            String name = "";

            // ПРОВЕРКА НА ПУСТОЕ НАЗВАНИЕ
            while (name.isEmpty()) {
                System.out.println("Введите название автомобиля № " + (i + 1));
                name = scanner.nextLine().trim();
                if (name.isEmpty()) {
                    System.out.println("Вы ввели пустое значение, попробуйте снова");
                }
            }
            // ВВОД СКОРОСТИ
            int speed = 0;
            while (true) {
                System.out.print("Введите скорость автомобиля от 0 до 250 км/ч: ");

                if (scanner.hasNextInt()) {
                    speed = scanner.nextInt();
                    scanner.nextLine();

                    if (speed >= 0 && speed <= 250) {
                        break;
                    } else {
                        System.out.println("Скорость автомобиля должна быть от 0 до 250 км/ч");
                    }
                } else {
                    System.out.println("Введите целое числовое значение, пожалуйста");
                    scanner.nextLine();
                }
            }
            autos[i] = new Auto(name, speed);
        }
        for (Auto auto : autos) {
            drive.newLeader(auto);
        }
        // РАСЧЕТ ДИСТАНЦИЙ
        int[] distances = new int[3];
        for (int j = 0; j < 3; j++) {
            distances[j] = autos[j].calculationWay();
        }
        boolean equal = true;
        for (int j = 1; j < 3; j++) {
            if (distances[j] != distances[0]) {
                equal = false;
                break;
            }
        }
        if (equal) {
            System.out.println("\nВсе водители проехали одинаковое расстояние. Победителя нет.");
        } else {
            System.out.println("\nПобедитель: " + drive.getLeader());
            System.out.println("Пройденная дистанция: " + drive.getLeaderDistance() + " км");
        }
    }
}
class Auto {
String name;
int speed;

    public Auto (String name,int speed) {
        this.name = name;
        this.speed = speed;
    }
    public String getName() {
        return name;
    }

    public int calculationWay () {
        return (speed * 24);
    }
}

class Drive {
String leaderName = "";
int leaderWay =  0;

    // МЕТОД ДЛЯ ЛИДЕРА
    public void newLeader (Auto auto)   {
        // пройденный путь для лидера:
        int newLeaderWay = auto.calculationWay();
        // Сравнение
        if (newLeaderWay > leaderWay) {
            leaderName = auto.getName();
            leaderWay = newLeaderWay;
        }
    }
    public String getLeader() {
        return leaderName;
    }
    public int getLeaderDistance() {
        return leaderWay;
    }
}
