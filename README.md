# CarTask
SoftUniTask
///
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

namespace CarManufacturer
{
    public class StartUp
    {
        static void Main(string[] args)
        {
            List<Tire[]> tiresOfCars = new List<Tire[]>();
            List<Engine> enginesOfCars = new List<Engine>();
            List<Car> cars = new List<Car>();

            while (true)
            {
                string input = Console.ReadLine();

                if (input == "No more tires")
                {
                    break;
                }
                
                string[] tireData = input
                    .Split(" ", StringSplitOptions.RemoveEmptyEntries);

                // 2 2.6 3 1.6 2 3.6 3 1.6  -Line 4 tires info for each tire
                Tire[] tires = new Tire[4]
                {
                   new Tire(int.Parse(tireData[0]), double.Parse(tireData[1])),
                   new Tire(int.Parse(tireData[2]), double.Parse(tireData[3])),
                   new Tire(int.Parse(tireData[4]), double.Parse(tireData[5])),
                   new Tire(int.Parse(tireData[6]), double.Parse(tireData[7])),
                };

                tiresOfCars.Add(tires);                
            }

            while (true)
            {
                string input = Console.ReadLine();

                if (input == "Engines done")
                {
                    break;
                }

                string[]engineData = input.Split(" ", StringSplitOptions.RemoveEmptyEntries);
                int engineHP = int.Parse(engineData[0]);
                double engineCapacity = double.Parse(engineData[1]);

                Engine engine = new Engine(engineHP, engineCapacity);

                enginesOfCars.Add(engine);
            }           

            while (true)
            {
                string input = Console.ReadLine();

                if (input == "Show special")
                {
                    if (cars.Any())
                    {
                        foreach (var curCar in cars)
                        {
                            if (curCar.Year >= 2017 && curCar.Engine.HorsePower > 330
                                && curCar.Tires.Sum(y => y.Pressure) >= 9
                                && curCar.Tires.Sum(y => y.Pressure) <= 10)
                            {
                                curCar.Drive(20);
                                StringBuilder sb = new StringBuilder();
                                sb
                                    .AppendLine($"Make: {curCar.Make}")
                                    .AppendLine($"Model: {curCar.Model}")
                                    .AppendLine($"Year: {curCar.Year}")
                                    .AppendLine($"HorsePowers: {curCar.Engine.HorsePower}")
                                    .AppendLine($"FuelQuantity: {curCar.FuelQuantity:F1}");

                                Console.WriteLine(sb);
                            }
                        }
                    } 

                    break;
                }

                string[] carsData = input
                    .Split(" ", StringSplitOptions.RemoveEmptyEntries);

                string carMake = carsData[0];
                string carModel = carsData[1];
                int carYear = int.Parse(carsData[2]);
                double fuelQuantity = double.Parse(carsData[3]);
                double fuelConsumption = double.Parse(carsData[4]);
                int carEngineIdx = int.Parse(carsData[5]);
                int carTiresIdx = int.Parse(carsData[6]);


                if (carEngineIdx >= 0 && carEngineIdx < enginesOfCars.Count 
                    && carTiresIdx >= 0 && carTiresIdx < tiresOfCars.Count)
                {
                    Car car = new Car(carMake, carModel, carYear, fuelQuantity, fuelConsumption,
                    enginesOfCars[carEngineIdx], tiresOfCars[carTiresIdx]);
                    cars.Add(car);
                }                
            }
        }
    }
}
