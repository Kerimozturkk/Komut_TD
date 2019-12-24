# Komut_TD
![Komut_TD classD](https://user-images.githubusercontent.com/49280604/71390187-5d9b1c00-2610-11ea-9d25-0a256fe466f2.png)


Komut Tasarım Deseninde: Bir nesne üzerinde bir işleminin nasıl yapıldığını 
bilmediğimiz ya da kullanılmak istenen nesneyi tanımadığımız durumlarda,
yapılmak istenen işlemi bir nesneye dönüştürerek, 
alıcı nesne tarafından işlemin yerine getirilmesi sağlayabiliriz

    public interface Komut {
       void execute();
    }

Komut sınıfı projenin interface sınıfıdır. Bünyesinde execute fonksiyonunu
barındırır. Excute fonksiyonunda daha sonra 2 tane nesne sınıfı implamante edilecek.
Bu sınıflar televizyonu açıp, kapatma işlemleri için TvAcKomutu ve TvKapatKomut sınıflarıdır.

    private Televizyon tv = null; 

    public TvAcKomutu(Televizyon tv) { 

    this.tv = tv;

    } 
    public void execute() {

    this.tv.ac();
    } 
			
TvAcKomutu sınıfı bünyesinde görüldüğü gibi Televizyon isminde bir 
sınıf değişkeni tanımlayarak, execute() metodu icinde bu nesnenin 
ac() metodunu kullanıyoruz. 


    private Televizyon tv = null;

    public TvKapatKomutu(Televizyon tv) {

    this.tv = tv;

    } 
    public void execute(){

    this.tv.kapat();

    }

TvKapatKomutu ile TvAcKomutu sınıflarının yapısı tamamıyla aynıdır. Sadece implamente edilen 
execute metodunun içinde adında anlaşılacağı kapat() fonksiyonu kullanılmaktadır.

    public class Kumanda {
    public Komut[] tus = new Komut[2]; 
	
	public Kumanda() { 
		
		Televizyon tv = new Televizyon(); 
		tus[0] = new TvAcKomutu(tv); 
		tus[1] = new TvKapatKomutu(tv); 
		} 
	public void tusla(int i) 
	{ 
		if(i > tus.length || i < 0) 
		{ 
			throw new RuntimeException("" + "Tus gecersiz!"); 
		} 
		
		tus[i].execute(); 
		
	}

	}
	
En önemli sınıf Kumanda sınıfıdır. Yazılım Dizaynı burada kendini gösterir.Kumanda sınıfında, 
Komut interface sınıfından olan nesneleri barındırmak üzere bir dizi tanımlıyoruz. 
Bu array, kumanda aletinin sahip olduğu tuşları temsil etmektedir.Yani daha önce kullanılan 
fonksiyonları bir nevi isimlendirip ana sınıfta bu isimlendirmelere göre çağırıcağız.
Kumandanın iki tuşu mevcuttur. 
Sınıfın constructurında bir televizyon nesnesi oluşturuyoruz.Üzerinde işlemi gerçekleştireceğimiz
nesnemiz bu nesnedir. 
Bu nesneyi TvAcKomutu ve TvKapatKomutu sınıflarından birer nesne oluşturmak 
için constructur parametresi olarak kullanıyoruz. komut nesneleri, yapılmak 
istenen operasyonu bünyesinde barındıran nesneleri tanırlar Yani 
TvAcKomutu, Televizyon nesnesini tanımaktadır.
tusla fonksiyonu içerisinde ana sınıfta yanlış bir eşleşme yapılması durumun da bir hata fırlatması
için bir if koşulu bulundurmaktadır ve tuslama yapilabilmesi adına tanımladıgımız tus[] dizi için
execute fonksiyununu çalıştırır. Bu fonksiyonlar komut nesnelerince tanımlandığı için bu diziye
uygulanabilir.

    public class Test {

	  public static void main(String[] args) {

		
		Kumanda kumanda = new Kumanda(); 
		
		kumanda.tusla(0);  
		
		kumanda.tusla(1); 


	}

Kumanda aletinin sıfırıncı ve birinci tuşlarına basmak için Test sınıfını kullanıyoruz.
New operatörü ile yeni bir Kumanda nesnesi oluşturduktan sonra, tusla(0) ve 
tusla(1) metodları ile çalıştırıyoruz.

    public class Televizyon {
      public void ac() {
        System.out.println("TV acildi");
        }

		public void kapat() {
		System.out.println("TV kapatildi");
		}

		public void kanalDegistir() {
		}
	}
	
Televizyon sınıfında komut nesnelerinin yapmasını istediğimiz fonksiyonlar bulunmaktadır.
Test yani ana sınıfta bu fonksiyonların hiç birini belirtmeden çalıştırdığımız fonksiyonlar bu
sınıftadır.Kodlama yapılırken fonksiyonların ne iş yaptığından 
çok hangi tuşun altında hangi komutun
bulunduğunu bilmek önemlidir.Çoğu sınıfta yapılan işlemler 
Televizyon nesnesi üzerinden yapılmaktadır.


 
