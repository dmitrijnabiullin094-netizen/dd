# dd
 public class Program

{
    public static void Main(string[] args)
    {
        /*List<Weapon> weapons = new();
        weapons.Add(new Sword());
        weapons.Add(new RangedWeapon());
        weapons.Add(new MeleeWeapaon());
        weapons.Add(new Axe());
        weapons.Add(new Bow());
        weapons.Add(new Crossbow());
        List<RangedWeapon> weapons2 = new();
        weapons2.Add(new Bow());
        weapons2.Add(new Crossbow());


        var sword = new Sword();
        sword.GetInfo();
        var axe = new Axe();
        axe.GetInfo();
        var bow = new Bow();
        bow.GetInfo();
        var crossbow = new Crossbow();
        crossbow.GetInfo();


        sword.Attack();

        foreach (var weapon in weapons)
        {
            weapon.Attack();
        }*/
        Console.WriteLine("Привет друже!!!!!!!! ТЫ ГОТОВ СТАТЬ ШНЫРЕМ????????? Если да то выбери класс: \nrange or melee");
        string stely = Console.ReadLine();
        
        switch(stely)
        {
            case "range":
                Console.WriteLine("Ты выбрал козуальную хуйню \nВыбери с чем играть с bow или crossbow");
                string weapr = Console.ReadLine();
                if (weapr == "bow")
                {
                    Console.WriteLine("Характеристики лука: ");
                    var bow = new Bow();
                    bow.GetInfo();
                }
                else if (weapr == "crossbow")
                {
                    Console.WriteLine("Характеристики арбалета: ");
                    var crossbow = new Crossbow();
                    crossbow.GetInfo();
                }    
                    break;


            case "melee":
                Console.WriteLine("Ты выбрал хуйню со смертельным кульбитом \nС чем будешь играть axe orr sword????");
                string melee = Console.ReadLine();
                switch (melee)
                {
                    case "sword":
                        Console.WriteLine("Характеристики меча: ");
                        var sword = new Sword();
                        sword.GetInfo();
                        break;
                    case "axe":
                        Console.WriteLine("Характеристики акса: ");
                        var axe = new Axe();
                        axe.GetInfo();
                        break;
                }
                break;
        }  
       



    }
}



public abstract class Weapon
{
    public Weapon()
    {

    }

    public string Name { get; set; }
    public int Weight { get; set; }
    public int BaseDamage { get; set; }
    public int Durability { get; set; }
    public abstract void Attack();
    public void Repair()
    {
        Console.WriteLine("Repairing...");
        Durability = 100;
        Console.WriteLine("Прочность полностью восстановлена");
    }
    public virtual string GetInfo()
    {
        string info = $"Name: {Name}, Weight: {Weight}, BaseDamage: {BaseDamage}, Durability: {Durability}";
        Console.WriteLine(info);
        return info;

    }

}
public class MeleeWeapaon : Weapon
{
    public int Reach { get; set; }
    public int AttackSpeed { get; set; }

    public override void Attack()
    {
        Durability = -BaseDamage;
        Console.WriteLine($"Атака мечом наносит {BaseDamage} урона. осталось - {Durability}");
    }
    public override string GetInfo()
    {
        string info = $"{base.GetInfo()}, Reach: {Reach}, AttackSpeed: {AttackSpeed}";
        Console.WriteLine(info);
        return info;
    }
    public void Block()
    {
        Random r = new Random();
        int h = r.Next(0, 1);
        if (h == 0)
        {
            Console.WriteLine("Блокировка не удалась. Получаешь полную мощность маслины");
        }
        else if (h == 1)
        {
            Console.WriteLine("Блок удался");
        }
    }


}
public class RangedWeapon : Weapon
{

    public int MaxAmmo { get; set; }
    public int CurrentAmmo { get; set; }
    public int EffectiveRange { get; set; }
    public void Reload()
    {
        MaxAmmo = 15;
        Console.WriteLine("Перезарядка...");
        CurrentAmmo = MaxAmmo;
        Console.WriteLine($"Колчан полон в колчане {CurrentAmmo} стрел ");
    }
    public void Aim()
    {
        Random r = new Random();
        int h = r.Next(0, 1);
        if (h == 0)
        {
            Console.WriteLine("Прицеливание не удалось. Урон не повышен.");
        }
        else if (h == 1)
        {
            BaseDamage = +((BaseDamage / 100) * 20);
            Console.WriteLine("Прицеливание удалось. Урон повышен на 20%");
        }
    }
    public override void Attack()
    {
        if (CurrentAmmo> 0)
        {
            CurrentAmmo--;
            Durability = -BaseDamage;
            Console.WriteLine("Патронов достаточно для атаки.");
        }
        else
        {
            Console.WriteLine("Ох батюшки, мы скребли по сусекам, а в колчане не осталось стрел/болтов. что же теперь делать? возможно есть специальная команда в консоли которая перезаряжает нашу хуйню в руке");
        }
    }
    public override string GetInfo()
    {
        string info = $"{base.GetInfo()}, CurrentAmmo: {CurrentAmmo}, EffectiveRange: {EffectiveRange}";
        Console.WriteLine(info);
        return info;
    }
}



public class Sword : MeleeWeapaon
{

    public int Material { get; set; }
    public int DamageType { get; set; }
    public override void Attack()
    {
        base.Attack();
        Random r = new Random();
        int h = r.Next(0, 1);
        if (h == 0)
        {
            Console.WriteLine("Ооооооо нет оочень крутое спец поведение не удалось, блииииннн. ох охохохохо блябляблябля, я уже злой");
        }
        else if (h == 1)
        {
            Console.WriteLine("Наш меч превозглашенный великим королем карлом петровичем 3им был использован против нечести зовущей себя дедушка 5, я барабанщик и дальтоник, поэтому использую свой  меч в благих целях, для упокоения душ и это МОЯ ИСТОРИЯ");
        }

    }

    public void SpecialAbility()
    {

    }
}


public class Axe : MeleeWeapaon
{
    public int Material { get; set; }
    public int DamageType { get; set; }
    public void SpecialAbility()
    {
        //hookshot
    }
}

public class Crossbow : RangedWeapon
{
    public int AmmoType { get; set; }
    public void SpecialAbility()
    {
        //multishot
    }

}
public class Bow : RangedWeapon
{
    public int AmmoType { get; set; }
    public override void Attack()
    { }
    public void SpecialAbility()
    {
        //  disarm
    }
}
