// Classe Singleton
public class Singleton {
    private static Singleton instance;

    // Construtor privado para evitar instanciamento externo
    private Singleton() {
    }

    // Método para obter a instância única
    public static Singleton getInstance() {
        if (instance == null) {
            instance = new Singleton();
        }
        return instance;
    }

    public void showMessage() {
        System.out.println("Hello from Singleton!");
    }
}

// Classe de teste
public class Main {
    public static void main(String[] args) {
        Singleton singleton = Singleton.getInstance();
        singleton.showMessage();
    }
}
import java.util.ArrayList;
import java.util.List;

// Interface Component
interface Component {
    void operation();
}

// Classe Leaf
class Leaf implements Component {
    private String name;

    public Leaf(String name) {
        this.name = name;
    }

    @Override
    public void operation() {
        System.out.println("Leaf: " + name);
    }
}

// Classe Composite
class Composite implements Component {
    private List<Component> children = new ArrayList<>();

    public void add(Component component) {
        children.add(component);
    }

    public void remove(Component component) {
        children.remove(component);
    }

    @Override
    public void operation() {
        System.out.println("Composite:");
        for (Component child : children) {
            child.operation();
        }
    }
}

// Classe de teste
public class Main {
    public static void main(String[] args) {
        Composite composite = new Composite();
        composite.add(new Leaf("Leaf 1"));
        composite.add(new Leaf("Leaf 2"));

        Composite composite2 = new Composite();
        composite2.add(new Leaf("Leaf 3"));
        composite2.add(composite); // Adiciona um composite

        composite2.operation();
    }
}
import java.util.ArrayList;
import java.util.List;

// Interface Observer
interface Observer {
    void update(String message);
}

// Classe Subject
class Subject {
    private List<Observer> observers = new ArrayList<>();
    private String state;

    public void addObserver(Observer observer) {
        observers.add(observer);
    }

    public void removeObserver(Observer observer) {
        observers.remove(observer);
    }

    public void setState(String state) {
        this.state = state;
        notifyObservers();
    }

    private void notifyObservers() {
        for (Observer observer : observers) {
            observer.update(state);
        }
    }
}

// Classe ConcreteObserver
class ConcreteObserver implements Observer {
    private String name;

    public ConcreteObserver(String name) {
        this.name = name;
    }

    @Override
    public void update(String message) {
        System.out.println(name + " received update: " + message);
    }
}

// Classe de teste
public class Main {
    public static void main(String[] args) {
        Subject subject = new Subject();

        ConcreteObserver observer1 = new ConcreteObserver("Observer 1");
        ConcreteObserver observer2 = new ConcreteObserver("Observer 2");

        subject.addObserver(observer1);
        subject.addObserver(observer2);

        subject.setState("State 1");
        subject.setState("State 2");
    }
}