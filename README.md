# Prototype Tasarım Deseni
Prototype (prototip) tasarım deseni creational grubununa ait, var olan nesnelerin kopyasının üretiminden sorumlu tasarım desenidir.

Bazı nesnelerin üretilme maliyeti oldukça yüksek olabilir. Veya aynı değerlerde nesne üretilmesi gereken durumlar olabilir. Böyle nesnelerin üretim maliyetini azaltmak için var olan nesnenin kopyasının üretilmesi yoluna gidilebilinir. Prototype tasarım deseni böyle durumdaki nesnelerin yönetilmesini sağlar. Buradaki kopyalama işlemi “Deep Copy – Derin Kopyalama” şeklindedir, yani nesne bire bir kopyalanarak yeni referans değerlere atanır.  Prototype tasarım deseni uygulanması oldukça basittir. İlk olarak içinde kendi türünde değer döndüren bir metot tanımlanmış olan interface veya abstract sınıf tanımlıyoruz. Çalışma zamanında kopyası alınabilecek nesnelerde bu interface veya abstract sınıfı uyguluyoruz. Concrete yani gerçek nesnelerde overwrite ettiğimiz bu metotlarda deep copy işlemini object sınıfında protected olarak tanımlanmış olan MemberwiseClone metodu ile gerçekleştirebiliriz. Concrete prototype sınıflarının farklı property veya metotları da olabilir.

Prototype tasarım deseninde 3 nesne yapısı vardır.

Prototype: Klonlama yapılacak sınıfların uygulaması gereken interface veya abstract sınıf.

Concrete Prototype: Klonlama özelliği olacak gerçek sınıflar.

Client: Klonlanmış nesneyi elde edecek nesne.

Kodumun sınıf diagramı ise şu şekilde

![Class Diagram](https://github.com/glahkerez/Yaz-l-m-MimarisiVeTasar-m-/blob/master/Prototype_class.png)

İlk olarak uygulamamızın Prototype ve ConcretePrototype nesnelerini yazalım.
 
public interface IPrototype
{
    IPrototype Clone();
}
 
public class Kisi : IPrototype
{
    public string Ad { get; set; }
    public DateTime DogumTarihi { get; set; }
 
    public IPrototype Clone()
    {
        return this.MemberwiseClone() as IPrototype;
    }
}
 
public class Urun : IPrototype
{
    public string Name { get; set; }
    public float Price { get; set; }
 
    public IPrototype Clone()
    {
        return this.MemberwiseClone() as IPrototype;
    }
}
 
Oluşturduğumuz desen aşağıdaki gibi kullanılabilinir.
 
static void Main(string[] args)
{
    Kisi k = new Kisi { Ad = "Ahmet", DogumTarihi = DateTime.Now };
    Kisi k2 = k.Clone() as Kisi;
    k2.Ad = "Mehmet";
 
    Console.WriteLine(k.Ad);
    Console.WriteLine(k2.Ad);
 
    Urun u = new Urun { Name = "Cep Telefonu XWZ19", Price = 100.00f };
    Urun u2 = u.Clone() as Urun;
    u2.Name = "Buzdolabı X999";
 
    Console.WriteLine(u.Name);
    Console.WriteLine(u2.Name);
 
    Console.ReadKey();
}

