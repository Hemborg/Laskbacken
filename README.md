# Laskbacken
Dryckesbacken Hermods skoluppgift, används också på csharpskolan

using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace sodacrate
{

    
    //Skapar en ny klass vid namn Sodacan som ska innehålla metoder för flaskor så att ett objekt skall kunna skapas här                     //som skall stoppas in i läskbacksvektorn.
    
    class Sodacan 
    
  //Lägger samtliga variabel-fält som private så att de inte är nåbara för andra klasser
  {
 
        private string nameonbottle;  
        private string typeonbottle;
        private int priceonbottle; 

     
        //En konstruktor för mina variabler
        
        public Sodacan(string name, string type, int priceeach)
        {
            nameonbottle = name;
            typeonbottle = type;
            priceonbottle = priceeach;
        }
        
        //Get -Set property för att göra variablarna publika och tillgängliga för andra klasser, förstod först inte nödvändigheten av           //dessa get set -propertys, men efter att ha läst på en del om dem förstod jag hur användbara de kan vara för att sätta format,         //vad som skall tillåtas för varje variabel som input.
        
        public string BottleName
        {
            get { return nameonbottle; }
            set { nameonbottle = value; }
        }

        public string BottleType
        {
            get { return typeonbottle; }
            set { typeonbottle = value; }
        }

        public int BottlePrice
        {
            get { return priceonbottle; }
            set { priceonbottle = value; }
        }

    }



    //KLASSEN Sodacrate, innehåller huvudmeny med metoder för alla val, samt skapande av vektorn som håller objekten från klassen           //sodacan
    
    class Sodacrate
    
    {
        //Initierar en vektor som skall innhålla objekt som skapas i klassen Sodacan, alltså själva läsken med de tre egenskaperna,             //variablerna.
        
        private Sodacan[] crateVector;

        
        //Håller reda på antal flaskor som stoppas in i backen
        private int antal_flaskor = 0; 

        public Sodacrate()
        {
            //Skapar vektorn med plats för 24 objekt från klassen Sodacan
            crateVector = new Sodacan[24];
        }
        //Körs när objektet skapas
        
        
        public void Run()
        {

            
            
            int temp = 0;

            do
            {
                Console.WriteLine("Välkommen till dryckesback-administratören!");
                Console.WriteLine("1. Lägg till en dryck i din dryckesback.");
                Console.WriteLine("2. Se vad som finns i backen.");
                Console.WriteLine("3. Se det totala priset.");
                Console.WriteLine("4. Avsluta programmet.");

                try
                {
                    temp = int.Parse(Console.ReadLine());//Konverterar användarens input till en inten temp som finns skapad utanför loopen
                }

                catch
                {
                    Console.WriteLine("\n");
                }
                switch (temp)//Använder intvariabeln temp för att läsa in vilket val användaren gör
                {
                    case 1:
                        add_soda();//Metodanrop beroende på val
                        break;

                    case 2:
                        print_crate();
                        break;

                    case 3:
                        calc_total();
                        break;

                    case 4:
                        Console.WriteLine("Avslutar...");
                        break;

                    default:
                        Console.WriteLine("\n##-- Välj något av alternativen 1 till 4. --##\n");
                        break;
                }  

            }while (temp != 4);//Kanske inget bra vilkor? Förstår att jag kan bryta denna med en bool också, men gillar inte, skadad från vårt andra uppdrag tror jag det va, att tvångsbryta loopar på det sättet, så försökte hitta ett villkor som var bättre lämpat.

        }





        public void add_soda()//Metod som LÄGGER TILL EN DRYCK
        {
            int temp2 = 0;

            if (antal_flaskor < 24)//Om backen inte är full
            {
                Console.WriteLine("Välj vilken dryck du vill lägga in i din dryckesback:");
                Console.WriteLine("1. XL-Cola");
                Console.WriteLine("2. Dr Pepper");
                Console.WriteLine("3. Hallonsoda");

                

                try
                {

                    temp2 = int.Parse(Console.ReadLine());
                }

                catch
                {
                    Console.WriteLine("\n");
                }
                
                switch (temp2)//Meny för val av dryck
                { 
                
                    case 1:
                        Console.WriteLine("\n##-- Lägger till en XL Cola... --##\n");
                        crateVector[antal_flaskor] = new Sodacan("XL Cola, ", "Dricka", 25);//Skapar ett objekt av klassen sodacan som innhehåller informationen som vi sagt att varje objekt av den klassen ska innehålla och stoppar in den i vektorn crateVector på position som hålls reda på av inten antal flaskor.
                        antal_flaskor++;
                        break;

                    case 2:
                        Console.WriteLine("\n##-- Lägger till en Dr Pepper...  --##\n");
                        crateVector[antal_flaskor] = new Sodacan("Dr pepper, ", "Dricka", 20);
                        antal_flaskor++;
                        break;

                    case 3:
                        Console.WriteLine("\n##-- Lägger till en Hallonsoda... --##\n");
                        crateVector[antal_flaskor] = new Sodacan("Hallonsoda, ", "Dricka", 15);
                        antal_flaskor++;
                        break;

                    default:
                        Console.WriteLine("\n##-- Välj något av alternativen 1 till 3. --##\n");
                        break;
                }

            }

            

            else
                Console.WriteLine("\n##-- Nu är drickabacken helt full! --##\n");//Om backen redan är full
           
        }





        public void print_crate()//Metod för att SE VAD SOM FINNS I BACKEN (Ville få in en foreach loop i programmet för att testa det, jag inser att jag kunnat lägga nrOfSodas varibelökningen under samma for-loop som det andra)
        {
            int nrOfSodas = 0;//Tre variabler för denna metod, 1 för att hålla reda på hur många slots/indexposter som är använda
            string whatIsInTheCrate = "";//En annan som sparar namnvariabeln på objekten på de platser som är fyllda
            int nrOfEmptySlots = 0;//Den tredje sparar antalet tomma platser

                foreach (var Sodacan in crateVector)//Dundrar igång en foreach loop som går igenom dryckesbacken
                {
                    if (Sodacan != null)
                        nrOfSodas += 1;//För varje plats som inte är tom, plussa på 1 på variabeln nrOfSodas
                        
                }

                
                for (int i = 0; i < crateVector.Length; i++)//Men man vill ju också veta vad det är i backen, så loopar en gång till...
                {

                if (crateVector[i] != null)
                    whatIsInTheCrate = crateVector[i].BottleName + whatIsInTheCrate;//...fast denna gång i jakt på BottleName variabeln i objekten som ligger i vektorn, sparar dem i variabeln whatsInTheCrate, för att presentera dem samlat.

                else
                    nrOfEmptySlots++;//Om platsen är tom adderar jag 1 till variabeln för tomma platser, för att kunna presentera hur många lediga platser som finns i utskriften.
                           

                }
                Console.WriteLine("\n##-- Just nu har du {0} drycker i backen: {1} --##\n\n##-- Du har fortfarande plats för {2} drycker till i backen! --##\n", nrOfSodas, whatIsInTheCrate, nrOfEmptySlots);//Presenterar de tre variablerna på ett trevligt sätt!

        }





       public void calc_total()//Räkna ut summan av allt i backen
       {
            int totalprice = 0;//Int som skall presentera slutsumman, allt adderas till denna
            for (int i = 0; i < antal_flaskor; i++)//Loopar igenom de fyllda delarna av vektorn, begränsat av variabeln antal_flaskor...
            {
                totalprice += crateVector[i].BottlePrice; //...i jakt på informationen BottlePrice, som finns i objektet Sodacan på varje "fylld" plats i vektorn "crateVector"
            }

            Console.WriteLine("\n##-- Den totala kostnaden av dina flaskor är {0} kr --##\n", totalprice); // skriver ut informationen från int:en totalprice, där vi har adderat BottlePrice-variabeln för varje objekt i loopen
       }


    }




    class Program
    {
        public static void Main(string[] args)
        {
            Sodacrate sodacrate = new Sodacrate();
            sodacrate.Run();
            
        }
    }
}
