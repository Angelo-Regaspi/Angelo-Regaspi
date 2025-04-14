using System;
using System.Linq;

class Program
{
    static void Main()
    {
        const int Students = 5;
        const int Subjects = 3;

        int[] grades = { 75, 60, 78, 
                         90, 77, 90,
                         82, 89, 82, 
                         97, 90, 91,
                         78, 81, 88 };

        Console.WriteLine("Student Grades:");
        DisplayGrades(grades, Students, Subjects);

        Console.WriteLine("\nGrade for Each Student:");
        DisplayStudentAverages(grades, Students, Subjects);

        Console.WriteLine("\nHighest Grade for Each Subject:");
        DisplayHighestGrades(grades, Students, Subjects);

        Console.WriteLine("\nLowest Grade for Each Subject:");
        DisplayLowestGrades(grades, Students, Subjects);

        Console.WriteLine("\nMedian Grade for Each Subject:");
        DisplayMedianGrades(grades, Students, Subjects);

        Console.WriteLine("\nHonor Students:");
        DisplayHonorStudents(grades, Students, Subjects);
    }

    static void DisplayGrades(int[] grades, int students, int subjects)
    {
        for (int i = 0; i < students; i++)
        {
            for (int j = 0; j < subjects; j++)
            {
                Console.Write(grades[i * subjects + j] + "\t");
            }
            Console.WriteLine();
        }
    }

    static void DisplayStudentAverages(int[] grades, int students, int subjects)
    {
        for (int i = 0; i < students; i++)
        {
            int sum = 0;
            for (int j = 0; j < subjects; j++)
            {
                sum += grades[i * subjects + j];
            }
            int average = sum / subjects;
            double norsuGrade = ConvertToNorsuGrade(average);
            string status = (norsuGrade <= 3.0) ? "Passed" : "Failed";
            Console.WriteLine($"Student {i + 1}: Average = {average}, NORSU Grade = {norsuGrade}, Status: {status}");
        }
    }

    static void DisplayHighestGrades(int[] grades, int students, int subjects)
    {
        for (int j = 0; j < subjects; j++)
        {
            int highest = grades[j];
            for (int i = 1; i < students; i++)
            {
                if (grades[i * subjects + j] > highest)
                {
                    highest = grades[i * subjects + j];
                }
            }
            Console.WriteLine($"Subject {j + 1}: {highest}");
        }
    }

    static void DisplayLowestGrades(int[] grades, int students, int subjects)
    {
        for (int j = 0; j < subjects; j++)
        {
            int lowest = grades[j];
            for (int i = 1; i < students; i++)
            {
                if (grades[i * subjects + j] < lowest)
                {
                    lowest = grades[i * subjects + j];
                }
            }
            Console.WriteLine($"Subject {j + 1}: {lowest}");
        }
    }

    static void DisplayMedianGrades(int[] grades, int students, int subjects)
    {
        for (int j = 0; j < subjects; j++)
        {
            int[] subjectGrades = new int[students];
            for (int i = 0; i < students; i++)
            {
                subjectGrades[i] = grades[i * subjects + j];
            }
            Array.Sort(subjectGrades);
            double median;
            int mid = students / 2;
            if (students % 2 == 0)
                median = (subjectGrades[mid - 1] + subjectGrades[mid]) / 2.0;
            else
                median = subjectGrades[mid];

            Console.WriteLine($"Subject {j + 1}: {median}");
        }
    }

    static void DisplayHonorStudents(int[] grades, int students, int subjects)
    {
        for (int i = 0; i < students; i++)
        {
            int sum = 0;
            for (int j = 0; j < subjects; j++)
            {
                sum += grades[i * subjects + j];
            }
            int average = sum / subjects;
            double norsuGrade = ConvertToNorsuGrade(average);
            if (norsuGrade <= 1.75)
            {
                Console.WriteLine($"Student {i + 1}: Average = {average}, NORSU Grade = {norsuGrade}, Status: Honor Student");
            }
        }
    }

    static double ConvertToNorsuGrade(int grade)
    {
        if (grade >= 96) return 1.0;
        if (grade >= 93) return 1.25;
        if (grade >= 90) return 1.5;
        if (grade >= 87) return 1.75;
        if (grade >= 84) return 2.0;
        if (grade >= 81) return 2.25;
        if (grade >= 78) return 2.5;
        if (grade >= 75) return 2.75;
        return 5.0;
    }
}
