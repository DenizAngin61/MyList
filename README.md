# MyList

import java.util.Arrays;

public class MyList<T> {
    private T[] array;
    private int size;

    // Varsayılan kapasite
    private static final int DEFAULT_CAPACITY = 10;

    // Varsayılan kapasite ile başlatan kurucu
    public MyList() {
        this.array = (T[]) new Object[DEFAULT_CAPACITY];
        this.size = 0;
    }

    // Özel kapasite ile başlatan kurucu
    public MyList(int capacity) {
        if (capacity <= 0) {
            throw new IllegalArgumentException("Kapasite sıfırdan büyük olmalı!");
        }
        this.array = (T[]) new Object[capacity];
        this.size = 0;
    }

    // Mevcut eleman sayısını döndürür
    public int size() {
        return size;
    }

    // Maksimum kapasiteyi döndürür
    public int capacity() {
        return array.length;
    }

    // Listeye eleman ekler
    public void add(T data) {
        if (size == array.length) {
            resizeArray();
        }
        array[size++] = data;
    }

    // Belirtilen indeksteki elemanı döndürür
    public T get(int index) {
        if (index < 0 || index >= size) {
            return null;
        }
        return array[index];
    }

    // Belirtilen indeksteki elemanı günceller
    public void set(int index, T data) {
        if (index >= 0 && index < size) {
            array[index] = data;
        } else {
            System.out.println("Geçersiz indeks: " + index);
        }
    }

    // Listeyi temizler
    public void clear() {
        array = (T[]) new Object[DEFAULT_CAPACITY];
        size = 0;
    }

    // Listede belirtilen elemanın indeksini döndürür (ilk eşleşme)
    public int indexOf(T data) {
        for (int i = 0; i < size; i++) {
            if (array[i].equals(data)) {
                return i;
            }
        }
        return -1;
    }

    // Listede belirtilen elemanın son indeksini döndürür
    public int lastIndexOf(T data) {
        for (int i = size - 1; i >= 0; i--) {
            if (array[i].equals(data)) {
                return i;
            }
        }
        return -1;
    }

    // Liste boş mu kontrolü
    public boolean isEmpty() {
        return size == 0;
    }

    // Listeyi belirli bir aralıkta alt liste olarak döndürür
    public MyList<T> subList(int start, int end) {
        if (start < 0 || end > size || start > end) {
            throw new IndexOutOfBoundsException("Geçersiz aralık!");
        }
        MyList<T> subList = new MyList<>(end - start);
        for (int i = start; i < end; i++) {
            subList.add(array[i]);
        }
        return subList;
    }

    // Listede belirtilen eleman var mı kontrolü
    public boolean contains(T data) {
        return indexOf(data) != -1;
    }

    // Listeyi dizi olarak döndürür
    public T[] toArray() {
        return Arrays.copyOf(array, size);
    }

    // Yardımcı metot: Diziyi yeniden boyutlandırır
    private void resizeArray() {
        int newCapacity = array.length * 2;
        array = Arrays.copyOf(array, newCapacity);
    }

    // Listeyi String olarak yazdırma
    @Override
    public String toString() {
        if (size == 0) {
            return "[]";
        }
        StringBuilder sb = new StringBuilder("[");
        for (int i = 0; i < size; i++) {
            sb.append(array[i]);
            if (i < size - 1) {
                sb.append(", ");
            }
        }
        sb.append("]");
        return sb.toString();
    }
}


Test Sınıfı

import java.util.Arrays;

public class Main {
    public static void main(String[] args) {
        MyList<Integer> list = new MyList<>();

        // Eleman ekleme
        list.add(10);
        list.add(20);
        list.add(30);
        list.add(40);
        list.add(50);

        System.out.println("Liste: " + list);
        System.out.println("Boyut: " + list.size());
        System.out.println("Kapasite: " + list.capacity());

        // Eleman erişimi ve güncelleme
        System.out.println("2. indeks: " + list.get(2));
        list.set(2, 35);
        System.out.println("2. indeksi güncelle: " + list);

        // Listeyi temizleme
        System.out.println("Liste boş mu? " + list.isEmpty());
        list.clear();
        System.out.println("Liste temizlendi: " + list);

        // Yeni elemanlar ekleyelim
        list.add(15);
        list.add(25);
        list.add(35);

        // Alt liste alma
        MyList<Integer> subList = list.subList(0, 2);
        System.out.println("Alt Liste: " + subList);

        // Eleman arama
        System.out.println("25 içeriyor mu? " + list.contains(25));
        System.out.println("25'in indeksi: " + list.indexOf(25));

        // Son indeks
        list.add(25);
        System.out.println("25'in son indeksi: " + list.lastIndexOf(25));

        // Listeyi diziye çevirme
        Integer[] array = list.toArray();
        System.out.println("Dizi olarak: " + Arrays.toString(array));
    }
}
