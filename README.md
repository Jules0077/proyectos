proyecto creados por simple practica personal


using proyecto_consola;
using System;
using System.Collections.Generic;
using System.IO;
using System.Media;
using System.Runtime.InteropServices;
using System.Threading;
//proyecto sin completa optimizacion ni "pulido" alguno
namespace proyecto_consola
{
    class Program
    {
        static void Main(string[] args)
        {
            #region Apertura De Archivos
            List<Vehiculo> listaVehiculos = new List<Vehiculo>();
            List<enemigo> ListaDeEnemigos = new List<enemigo>();

            Console.WriteLine("Hola mundo");
            SoundPlayer player = new SoundPlayer("C:\\Users\\Elian\\Desktop\\otros(borrar)\\proyecto consola\\beats.wav");
            player.PlayLooping();
            player.Stop();//borrar esta linea despues.
            // Cargar la lista de vehículos desde un archivo si existe
            try
            {
                if (File.Exists("vehiculos.txt"))
                {
                    listaVehiculos.Clear(); // Limpiar la lista actual
                    using (StreamReader reader = new StreamReader("vehiculos.txt"))//abre el archivo
                    {
                        string line;
                        while ((line = reader.ReadLine()) != null)//verifica que el archivo no este vacio
                        {
                            string[] partes = line.Split(',');//si hago que esto tenga un punto(".") y hago que se guarde
                            //como un punto(".") en su creacion(streamwriter)
                            int id = int.Parse(partes[0]);
                            string marca = partes[1];
                            string modelo = partes[2];
                            float km = float.Parse(partes[3]);
                            float precio = float.Parse(partes[4]);

                            Vehiculo vehiculo = new Vehiculo();
                            vehiculo.Fabricar(id, marca, modelo, km, precio);
                            listaVehiculos.Add(vehiculo);
                        }
                    }
                }
            }
            catch
            {
                Console.WriteLine("se rompio todo master");
                Thread.Sleep(1000);
            }
            #endregion
            // Cargar la lista de vehículos desde un archivo si existe
            try
            {
                if (File.Exists("Enemigos.txt"))
                {
                    ListaDeEnemigos.Clear(); // Limpiar la lista actual
                    using (StreamReader reader = new StreamReader("Enemigos.txt"))//abre el archivo
                    {
                        string line;
                        while ((line = reader.ReadLine()) != null)//verifica que el archivo no este vacio
                        {
                            string[] partes = line.Split(',');//si hago que esto tenga un punto(".") y hago que se guarde
                            //como un punto(".") en su creacion(streamwriter)
                            string nombre = partes[0];
                            int vida = int.Parse(partes[1]); 
                            int daño = int.Parse(partes[2]); 
                            int defensa = int.Parse(partes[3]);

                            enemigo Enemigo = new enemigo();
                            Enemigo.spawn(nombre, vida, daño, defensa);
                            ListaDeEnemigos.Add(Enemigo);
                        }
                    }
                }
            }
            catch
            {
                Console.WriteLine("se rompio todo master");
                Thread.Sleep(1000);
            }
            //completar este try y arreglar el punto 7            
            while (true)
            {
                #region opciones
                Console.WriteLine("\n¿Qué desea hacer?");
                Console.WriteLine("1. Agregar un vehículo");
                Console.WriteLine("2. Mostrar lista de vehículos");
                Console.WriteLine("3. Ruleta rusa");
                Console.WriteLine("4. Control de sonido");
                Console.WriteLine("5. Dados");
                Console.WriteLine("6. Carrera de numeros");
                Console.WriteLine("7. crear enemigo");
                Console.WriteLine("8. Salir");
                int opcion = int.Parse(Console.ReadLine());
                Console.Clear();
                #endregion
                switch (opcion)
                {
                    case 1:
                        Vehiculo nuevoVehiculo = new Vehiculo();
                        Console.WriteLine("Ingrese ID del vehículo:");
                        int id = int.Parse(Console.ReadLine());
                        Console.WriteLine("Ingrese Marca del vehículo:");
                        string marca = Console.ReadLine();
                        Console.WriteLine("Ingrese Modelo del vehículo:");
                        string modelo = Console.ReadLine();
                        Console.WriteLine("Ingrese Kilometraje del vehículo:");
                        float kilometraje = float.Parse(Console.ReadLine());
                        Console.WriteLine("Ingrese Precio del vehículo:");
                        float precio = float.Parse(Console.ReadLine());

                        nuevoVehiculo.Fabricar(id, marca, modelo, kilometraje, precio);
                        listaVehiculos.Add(nuevoVehiculo);

                        // Guardar la lista de vehículos en un archivo
                        using (StreamWriter writer = new StreamWriter("vehiculos.txt"))
                        {
                            foreach (var vehiculo in listaVehiculos)
                            {
                                writer.WriteLine($"{vehiculo.Id},{vehiculo.Marca},{vehiculo.Modelo},{vehiculo.Km},{vehiculo.Precio}");
                            }
                        }

                        break;//añadir vehiculo
                    case 2:
                        Console.WriteLine("\nLista de Vehículos:");
                        foreach (var vehiculo in listaVehiculos)
                        {
                            Console.WriteLine($"ID: {vehiculo.Id}, Marca: {vehiculo.Marca}, Modelo: {vehiculo.Modelo}, Kilometraje: {vehiculo.Km}, Precio: {vehiculo.Precio}");
                        }
                        break;//lista de vehiculos
                    case 3:
                        bool eleccion = true;
                        while (eleccion == true)
                        {
                            try
                            {

                                Console.WriteLine("elija un numero entre el 1 y el 6");
                                int i = int.Parse(Console.ReadLine());
                                Random random = new Random();
                                int x = random.Next(1, 6);
                                string a;
                                if (x < 7 && x > 0)
                                {
                                    Console.WriteLine("cargando la bala...");
                                    Thread.Sleep(1000);
                                    for (int j = 0; j < 3; j++)
                                    {
                                        Console.WriteLine(".");
                                        Thread.Sleep(600);
                                    }
                                    Thread.Sleep(500);

                                    if (x == i)
                                    {
                                        Thread.Sleep(300);
                                        Console.WriteLine("BANG!!!");
                                        Console.WriteLine("te toco el numero " + x + "re dormiste");
                                        Console.WriteLine("intentar de nuevo?(s/n)");
                                        a = Console.ReadLine();

                                        if (a == "n")
                                        {
                                            eleccion = false;

                                        }
                                    }
                                    else
                                    {
                                        Console.WriteLine("CLANK!");
                                        Thread.Sleep(300);
                                        Console.WriteLine("salio el numero: " + x);
                                        Console.WriteLine("y elegiste el numero " + i + " safaste eh");
                                        Console.WriteLine("intentar de nuevo?(s/n)");
                                        a = Console.ReadLine();

                                        if (a == "n")
                                        {
                                            eleccion = false;

                                        }

                                    }
                                }
                                else
                                {
                                    Console.WriteLine("seleccione un numero valido.");
                                }
                            }
                            catch (Exception)
                            {
                                Console.Clear();
                                Console.WriteLine("Porfavor eliga un numero valido del 1 al 6.");
                            }
                        }
                        break;//ruleta rusa
                    case 4:
                        int OpcionSonido;
                        Console.WriteLine("seleccione una opcion");
                        Console.WriteLine("1. Encender musica.");
                        Console.WriteLine("2. Apagar musica");
                        OpcionSonido = int.Parse(Console.ReadLine());
                        switch (OpcionSonido)
                        {
                            case 1:
                                player.PlayLooping();
                                Console.Clear();
                                break;

                            case 2:
                                player.Stop();
                                Console.Clear();
                                break;

                            default:
                                Console.WriteLine("nada sucedio...");
                                break;
                        }

                        break;//opciones de sonido
                    case 5:
                        bool Dados = true;
                        //trucaso: cambiar las opciones por una funcion y trabajar conforme a funciones
                        while (Dados == true)
                        {
                            int OpcionDados;
                            Console.Clear();
                            Console.WriteLine("elija una opcion: ");
                            Console.WriteLine("1. reglas");
                            Console.WriteLine("2. jugar");
                            Console.WriteLine("3. salir");

                            OpcionDados = int.Parse(Console.ReadLine());
                            switch (OpcionDados)
                            {
                                case 1:
                                    Console.Clear();
                                    Console.WriteLine("la computadora selecciona un numero aleatorio");
                                    Console.WriteLine("entre el 1 y el 6, vos decidis si quedartelo y sumarlo a los puntos");
                                    Console.WriteLine("o si retirarte y no sumar nada, si el numero es 6 perdes si no seguis");
                                    Console.WriteLine("sumando puntos, mientras mas puntos mejor durante las 10 rondas");
                                    Console.ReadLine();
                                    break;//reglas
                                case 2:
                                    bool ReiniciarDados = true;
                                    while (ReiniciarDados == true)
                                    {
                                        Console.Clear();
                                        int puntos = 0;
                                        for (int ronda = 0; ronda <= 10; ronda++)
                                        {
                                            if (ronda != 10)
                                            {
                                                Console.Clear();
                                                Random RandNum = new Random();
                                                int x = RandNum.Next(1, 7);

                                                Console.WriteLine("descartar?s/n");
                                                Console.WriteLine("ronda numero:" + ronda);
                                                Console.WriteLine("puntos actuales: " + puntos);
                                                string Respuesta = Console.ReadLine();
                                                if (x == 6 && Respuesta == "s")
                                                {
                                                    Console.WriteLine("PERDISTE!!!");
                                                    Console.WriteLine("puntos totales: " + puntos);
                                                    Console.WriteLine("reiniciar?s/n");
                                                    string reinicio = "n";
                                                    reinicio = Console.ReadLine();
                                                    if (reinicio == "s")
                                                    {
                                                        puntos = 0;
                                                        Respuesta = "n";
                                                        ronda = 11;
                                                        reinicio = "n";


                                                    }
                                                    else if (reinicio == "n")
                                                    {
                                                        ronda = 11;
                                                        ReiniciarDados = false;
                                                    }
                                                }
                                                else if (Respuesta == "s")
                                                {
                                                    Console.WriteLine("puntos sumados: " + x);
                                                    puntos = puntos + x;

                                                }
                                                else if (Respuesta == "n")
                                                {


                                                }
                                                else
                                                {
                                                    Console.WriteLine("elija entre s o n.");
                                                    ronda = 0;
                                                    puntos = 0;
                                                }
                                            }
                                            else
                                            {

                                                Console.WriteLine("juego finalizado!");
                                                Console.WriteLine("Ronda numero: " + ronda);
                                                Console.WriteLine("puntos maximos: " + puntos);
                                                Console.ReadLine();
                                                ReiniciarDados = false;
                                            }
                                        }
                                    }
                                    break;//jugar

                                case 3:
                                    Dados = false;
                                    break;//salir
                            }
                        }

                        break;//dados
                    case 6:
                        bool ReiniciarJuegoCarrera = true;
                        while (ReiniciarJuegoCarrera == true)
                        {
                            int contador = 0;
                            int OpcionCarrera;
                            bool ReinicioCarera = true;
                            Console.WriteLine("elija una opcion: ");
                            Console.WriteLine("1. reglas");
                            Console.WriteLine("2. jugar");
                            Console.WriteLine("3. salir");
                            int NumeroCarrera;
                            OpcionCarrera = int.Parse(Console.ReadLine());
                            switch (OpcionCarrera)
                            {

                                case 1:
                                    Console.WriteLine("se elije un numero aleatorios y ");
                                    Console.WriteLine("se tiene que adivinar si el numero es");
                                    Console.WriteLine("mayor o menor al numero aleatorio entre 1 y 100");
                                    //continuar por aca

                                    break;

                                case 2:
                                    Random random = new Random();
                                    int x = random.Next(1, 101);

                                    while (ReinicioCarera == true)
                                    {
                                        try
                                        {
                                            Console.WriteLine("elegi un numero del 1 al 100");
                                            NumeroCarrera = int.Parse(Console.ReadLine());

                                            contador = contador + 1;
                                            Console.Clear();
                                            if (NumeroCarrera == x)
                                            {
                                                Console.WriteLine("le atinaste papu :D.");
                                                Console.WriteLine("GANASTE!!!");
                                                Console.WriteLine("lo conseguiste en " + contador + " rondas");
                                                ReinicioCarera = false;
                                                Console.WriteLine("Reiniciar?(s/n)");
                                                string respuesta = Console.ReadLine();
                                                if (respuesta == "s")
                                                {

                                                }
                                                else if (respuesta == "n")
                                                {
                                                    ReiniciarJuegoCarrera = false;
                                                }
                                            }
                                            else if (NumeroCarrera < x)
                                            {
                                                Console.WriteLine("un poco mas...");
                                                Console.WriteLine("------------------");
                                            }
                                            else if (NumeroCarrera > x)
                                            {
                                                Console.WriteLine("un poco menos...");
                                                Console.WriteLine("------------------");
                                            }
                                            Console.WriteLine("Elegi otro mas");
                                        }
                                        catch
                                        {
                                            Console.Clear();
                                            Console.WriteLine("elija un numero valido entre el 1 y el 100");
                                        }
                                    }
                                    Console.Clear();
                                    break;
                                case 3:
                                    break;

                            }
                        }

                        break;//carrera de numeros
                    case 7:
                        Console.WriteLine("Crear enemigo? (s/n)");
                        if (Console.ReadLine() == "s")
                        {
                            //creacion del enemigo
                            enemigo NuevoEnemigo = new enemigo();
                            Console.WriteLine("Ingrese nombre del enemigo:");
                            string nombre = Console.ReadLine();
                            Console.WriteLine("Ingrese vida:");
                            int vida = int.Parse(Console.ReadLine());
                            Console.WriteLine("Ingrese daño:");
                            int daño = int.Parse(Console.ReadLine());
                            Console.WriteLine("Ingrese defensa:");
                            int defensa = int.Parse(Console.ReadLine());

                            NuevoEnemigo.spawn(nombre, vida, daño, defensa);
                            ListaDeEnemigos.Add(NuevoEnemigo);
                            //guardado en lista
                            using (StreamWriter writer = new StreamWriter("Enemigos.txt"))
                            {
                                foreach (var enemigo in ListaDeEnemigos)
                                {
                                    writer.WriteLine($"{NuevoEnemigo.NombreEnemigo},{NuevoEnemigo.Vida},{NuevoEnemigo.Daño},{NuevoEnemigo.Defensa}");
                                }
                            }
                        }
                        else
                        {
                            Console.WriteLine("Enemigos cargados...");
                            
                            foreach (var enemigo in ListaDeEnemigos)
                            {
                                Console.WriteLine($"ID: {enemigo.NombreEnemigo}, Marca: {enemigo.Vida}, Modelo: {enemigo.Daño}, Kilometraje: {enemigo.Defensa}");
                            }
                        }
                        break;//rpg game
                    case 8:
                        Console.WriteLine("Gracias por usar el programa. ¡Hasta luego!");
                        return;//salir        
                    default:
                        Console.WriteLine("Opción no válida. Por favor, seleccione una opción válida.");
                        Console.ReadLine();
                        break;//aprende a escribir
                }
            }
            
        }
        public void RandomRoll(int a, int b, bool SiYNo)
        {
            Random TiradaRandom = new Random();
            if (SiYNo == true)//limitar tirada?
            {//si
                TiradaRandom.Next(a, b);
            }
            else//no
            {
                TiradaRandom.Next();
            }
        }

            

        }

        public class enemigo
        {
            public string NombreEnemigo { get; set; }
            public int Vida { get; private set; }
            public int Daño { get; private set; }
            public int Defensa { get; private set; }

            public void spawn(string nombreenemigo, int vida, int daño, int defensa)
            {
                NombreEnemigo = nombreenemigo;
                Vida = vida;
                Daño = daño;
                Defensa = defensa;
            }
        }
        public class Vehiculo
        {
            public int Id { get; private set; }
            public string Marca { get; private set; }
            public string Modelo { get; private set; }
            public float Km { get; private set; }
            public float Precio { get; private set; }

            public void Fabricar(int identificador, string marca, string modelo, float kilometro, float precio)
            {
                Id = identificador;
                Marca = marca;
                Modelo = modelo;
                Km = kilometro;
                Precio = precio;
            }
        }
    }
   

