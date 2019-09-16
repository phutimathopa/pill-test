using System;

namespace pillTestPart2
{
    internal class Program
    {
        private static Random random = new Random();

        private static void Main()
        {
            int changedBean = 0;
            int keepBean = 0;
            int count = 0;

            for (var index = 0; index < 100000; index++)
            {
                if (Game(false))
                {
                    keepBean += 1;
                }
                else
                    keepBean += 0;

                if (Game(true))
                {
                    changedBean += 1;
                }
                else
                    changedBean += 0;

                count++;
            }
            Console.WriteLine("keep Pill Tests: " + count + ", Died: " + keepBean + " times, Die Percentage: " + ((double)keepBean / count) * 100 + "%");
            Console.WriteLine("changed Pill Tests: " + count + ", Died: " + changedBean + " times, Die Percentage: " + ((double)changedBean / count) * 100 + "%");
            Console.ReadLine();
        }

        private static bool Game(bool switchBeans)
        {
            int beanPosition = GenerateSafeandPOisonus();
            int firstBean = GenerateFirstBeanChoice();
            int randomPoisnous = GenerateRandomBean(firstBean, beanPosition);
            int finalChoice;
            if (switchBeans)
            {
                finalChoice = SwitchBeans(firstBean, randomPoisnous);
            }
            else
            {
                finalChoice = firstBean;
            }

            return finalChoice == beanPosition;
        }

        private static int GenerateFirstBeanChoice()
        {
            int choice = random.Next(0, 3);
            return choice;
        }

        private static int GenerateSafeandPOisonus()
        {
            int beans = random.Next(0, 3);
            return beans;
        }

        private static int GenerateRandomBean(int firstBeanChoice, int beanPosition)

        {
            while (true)
            {
                int randomPoisonos = random.Next(0, 3);
                if (randomPoisonos == firstBeanChoice || randomPoisonos == beanPosition)
                {
                    continue;
                }
                return randomPoisonos;
            }
        }

        private static int SwitchBeans(int firstBeanChoice, int randomBeans)
        {
            int switchPillResult = 0;
            while (true)
            {
                if (switchPillResult == firstBeanChoice ||
                    switchPillResult == randomBeans)
                {
                    switchPillResult++;
                    continue;
                }
                return switchPillResult;
            }
        }
    }
}