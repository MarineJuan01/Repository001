# Repository001
using System;
using System.IO;
using System.Diagnostics;

namespace ConsoleApplication2
{
    class Program
    {
        public static void Main(string[] args)
        {
            int DirCount = Directory.GetDirectories("C:\\for checking", ".", SearchOption.AllDirectories).Length;
            int FilesCount = Directory.GetFiles("C:\\for checking", ".", SearchOption.AllDirectories).Length;
            if (DirCount >= 1)
            {
                Console.Write("There are "); Console.Write(DirCount); Console.WriteLine(" directories found:");
            }

            else if (DirCount < 1)
            {
                Console.WriteLine("There are no Directories found");
            }

            if (FilesCount >= 1)
            {
                Console.Write("There are "); Console.Write(FilesCount); Console.WriteLine(" files found:");
                Console.ReadLine();
            }
            else if (FilesCount < 1)
            {
                Console.WriteLine("There are no files found");
            }
            foreach (string entry in Directory.GetDirectories(@"C:\for checking\"))
            {
                DisplayFileSystemInfoAttributes(new DirectoryInfo(entry));
            }

            foreach (string entry in Directory.GetFiles(@"C:\for checking\"))
            {
                DisplayFileSystemInfoAttributes(new FileInfo(entry));
            }
            ////////////////////////////////////////////////////////////////////////////////////////////////////////////////////
            string[] files = Directory.GetFiles(@"C:\for checking\", "*.*", SearchOption.AllDirectories);
            foreach (string file in files)
            {
               
                

                    if (File.GetCreationTime(file)
                        < DateTime.Now.AddMonths(-3))
                    {
                        Console.WriteLine(files);
                        Console.ReadKey();
                        //File.Delete(file);

                    }

                

                else if (File.GetCreationTime(file) > DateTime.Now.AddMonths(-3))
                {

                    Console.WriteLine(files);
                    Console.ReadKey();

                }
            }
            ////////////////////////////////////////////////////////////////////////////////////////////////////////////////////
        }
        static void DisplayFileSystemInfoAttributes(FileSystemInfo fsi)
        {

            string entryType = "File";


            if ((fsi.Attributes & FileAttributes.Directory) == FileAttributes.Directory)
            {
                entryType = "Directory";
            }

            Console.WriteLine("{0} {1} was created on {2:D}", entryType, fsi.FullName, fsi.CreationTime);
            Console.ReadKey();
        }
        ////////////////////////////////////////////////////////////////////////////////////////////////////////////////////
    }
}
