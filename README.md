# Program Hitung Nilai Akhir Mahasiswa

## Deskripsi
Program ini menghitung **nilai akhir** dan **grade mahasiswa** berdasarkan nilai **Tugas**, **UTS**, dan **UAS**.  
Perhitungan dilakukan menggunakan bobot tetap:
- Tugas = 30%
- UTS = 30%
- UAS = 40%

Kelas utama adalah `NilaiAkhirMahasiswa`, yang mengimplementasikan interface `Nilai.HitungNilai`.

---

## Fitur
- Menggunakan **Encapsulation** untuk melindungi atribut.
- Menggunakan **Interface** untuk mendefinisikan kontrak perhitungan.
- Menggunakan **Konstanta (final)** untuk bobot nilai.
- Menghitung otomatis **Nilai Akhir** dan **Grade** berdasarkan rentang nilai.
- Menampilkan hasil dalam format tabel teks di konsol.

---

##  Struktur Kelas dan Me

- ```bash
    class NilaiAkhirMahasiswa implements Nilai.HitungNilai 
    ```
  Class ini ada class Utama / main 

- ```bash
    private String nama;
    private double tugas;
    private double uts;
    private double uas;
    private double nilaiAkhir;
    private String grade;
  ```
  Setelah itu akan dideklarasikan method ini dan di refactor rename untuk meperjelas kegunaan dari method tersebut


- Setelah itu method tersebut akan di refactor dengan encapsulation agar atribuat dapat dilindungin dan dapat menambahan get dan set serta contructor
  **Contoh get dan set** :
  ```bash
        public String getNama() {
        return nama;
    }

    public void setNama(String nama) {
        this.nama = nama;
    }

    public double getTugas() {
        return tugas;
    }

    public void setTugas(double tugas) {
        this.tugas = tugas;
    }

    public double getUts() {
        return uts;
    }

    public void setUts(double uts) {
        this.uts = uts;
    }

    public double getUas() {
        return uas;
    }

    public void setUas(double uas) {
        this.uas = uas;
    }

    public double getNilaiAkhir() {
        return nilaiAkhir;
    }

    public void setNilaiAkhir(double nilaiAkhir) {
        this.nilaiAkhir = nilaiAkhir;
    }

    public String getGrade() {
        return grade;
    }

    public void setGrade(String grade) {
        this.grade = grade;
    }

  ```
  
  **Dan contoh contructornya :**
  ```bash
        public void tampilkanData() {
        System.out.println("Nama Mahasiswa : " + getNama());
        System.out.println("Nilai Tugas    : " + getTugas());
        System.out.println("Nilai UTS      : " + getUts());
        System.out.println("Nilai UAS      : " + getUas());
        System.out.println("Nilai Akhir    : " + getNilaiAkhir());
        System.out.println("Grade          : " + getGrade());
    }
  ```
  
- Untuk Mnegitung Nilai akhir nya di gunakan rumus Nilai dikali persenannya, dan setelah itu akan di refactor Extract Method dan Extrack InterfaceSeperti ini:
    ```bash
    @Override
    public void hitungNilai() {
        setNilaiAkhir(getAkhir());

        if (getNilaiAkhir() >= 80) {
            setGrade("A");
        } else if (getNilaiAkhir() >= 70) {
            setGrade("B");
        } else if (getNilaiAkhir() >= 60) {
            setGrade("C");
        } else if (getNilaiAkhir() >= 50) {
            setGrade("D");
        } else {
            setGrade("E");
        }
    }

    private double getAkhir() {
        return (getTugas() * nilaiHitungTugas) + (getUts() * nilaiHitungUts) + (getUas() * nilaiHitungUas);
    }
    ```

  Setelah itu nilai hitungTugas akan di refactor Introduce Contant yang awalnya bernilai constanta menjadi nilaiHitungTugas  dan akan muncul deklarasi contanta dengan nilai yang sudah ditentukan seperti ini:
   ```bash
    public static final double nilaiHitungTugas = 0.3;
    public static final double nilaiHitungUts = 0.3;
    public static final double nilaiHitungUas = 0.4;
  ```
- Setelah itu bisa direfactor move mthod dimana class main di class utama dipindah ke class yang berdiri sendiri seperti ini:
     ```bash
    class MainApp{
    public static void main(String[] args) {
        Scanner input = new Scanner(System.in);
        String nama;
        double tugas, UTS, uas;

        System.out.print("Masukkan nama mahasiswa: ");
        nama = input.nextLine();
        System.out.print("Masukkan nilai tugas: ");
        tugas = input.nextDouble();
        System.out.print("Masukkan nilai UTS: ");
        UTS = input.nextDouble();
        System.out.print("Masukkan nilai UAS: ");
        uas = input.nextDouble();

        NilaiAkhirMahasiswa m = new NilaiAkhirMahasiswa(nama, tugas, UTS, uas);
        m.hitungNilai();
        m.tampilkanData();

        input.close();
      }
  }
  ```
  Di class ini kita tinggal mengimplemetasikan method di class utama ke class baru 