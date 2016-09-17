using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

namespace comienzo
{
    class finalizado
    {

        public void imprimir(string[] operacion)
        {


            Console.SetCursorPosition(1, 4); Console.WriteLine("El Resultado Es:");
            Console.SetCursorPosition(1, 5); Console.WriteLine("-------------------------------------");
            Console.SetCursorPosition(15, 6); Console.WriteLine(" " + operacion[1]);
            Console.SetCursorPosition(1, 7); Console.WriteLine("-------------------------------------");
            Console.ReadKey();
        }

    }

    class espacios
    {


        public void buscaresp(byte pcdo, byte opera, string[] operacion)
        {

            string cambio;
            pcdo -= 2;

            for (; opera <= pcdo; opera++)
            {
                if (operacion[opera] == " ")
                {
                    opera += 2;
                    cambio = operacion[opera];
                    opera -= 2;
                    operacion[opera] = cambio;
                    opera += 2;
                    operacion[opera] = " ";
                    opera -= 2;
                }
            }

        }


        public void organiza(byte pcdo, byte opera, string[] operacion)
        {

            byte ultimo = 0; string cambio; byte posb = 0;
            pcdo = 19;
            while (pcdo >= 1)
            {
                ultimo = pcdo;
                while (ultimo >= 1)
                {
                    posb = Convert.ToByte(ultimo - 1);
                    if (posb != 255)
                    {
                        while (((posb != 255) && (posb >= 0)) && (operacion[posb] == " "))
                        {
                            cambio = operacion[ultimo];
                            operacion[posb] = cambio;
                            operacion[ultimo] = " ";
                            posb--;
                        }
                    }
                    ultimo--;

                }

                pcdo--;
            }


        }


        public void parentesis(string[] operacion, byte pfin)
        {
            byte abierto = 0, pcdo = 0, opera = 0, a, b, k, contar;
            double x = 0, y = 0, resultado = 0;
            espacios organizar = new espacios();
            espacios acomodar = new espacios();

            while (abierto == 0)
            {
                for (byte i = 0; i <= pfin; i++)
                {
                    if ((operacion[i] == "("))
                    {
                        opera = i; pcdo = i; pcdo += 1;
                        while ((operacion[pcdo] != "(") && (operacion[pcdo] != ")"))
                        {
                            pcdo += 1;
                        }

                        if (operacion[pcdo] != "(")
                        {
                            byte j = Convert.ToByte(opera + 1);
                            for (; j <= pcdo; j++)
                            {
                                if (operacion[j] == "*")
                                {
                                    a = j; b = j;
                                    a -= 1; b += 1;
                                    x = Convert.ToDouble(operacion[a]); y = Convert.ToDouble(operacion[b]);
                                    resultado = x * y;


                                    a = j; b = j;
                                    a -= 1; b += 1;
                                    operacion[a] = Convert.ToString(resultado);
                                    operacion[j] = " "; operacion[b] = " ";
                                    j = a;
                                    organizar.buscaresp(pcdo, opera, operacion);
                                    acomodar.organiza(pcdo, opera, operacion);
                                    pcdo -= 2;
                                }
                                else
                                {
                                    if (operacion[j] == "/")
                                    {
                                        a = j; b = j;
                                        a -= 1; b += 1;
                                        x = Convert.ToDouble(operacion[a]); y = Convert.ToDouble(operacion[b]);
                                        resultado = x / y;
                                        a = j; b = j;
                                        a -= 1; b += 1;
                                        operacion[a] = Convert.ToString(resultado);
                                        operacion[j] = " "; operacion[b] = " ";
                                        j = a;
                                        organizar.buscaresp(pcdo, opera, operacion);
                                        acomodar.organiza(pcdo, opera, operacion);
                                        pcdo -= 2;
                                    }

                                }


                            }



                            j = Convert.ToByte(opera + 1);
                            for (; j <= pcdo; j++)///for-3 con este for realizo las operaciones segundarias
                            {
                                if (operacion[j] == "+")//if-4
                                {
                                    a = j; b = j;
                                    a -= 1; b += 1;
                                    x = Convert.ToDouble(operacion[a]); y = Convert.ToDouble(operacion[b]);
                                    resultado = x + y;
                                    a = j; b = j;
                                    a -= 1; b += 1;
                                    operacion[a] = Convert.ToString(resultado);
                                    operacion[j] = " "; operacion[b] = " ";
                                    j = a;
                                    organizar.buscaresp(pcdo, opera, operacion);
                                    acomodar.organiza(pcdo, opera, operacion);
                                    pcdo -= 2;
                                }
                                else
                                {
                                    if (operacion[j] == "-")
                                    {
                                        a = j; b = j;
                                        a -= 1; b += 1;
                                        x = Convert.ToDouble(operacion[a]); y = Convert.ToDouble(operacion[b]);
                                        resultado = x - y;


                                        a = j; b = j;
                                        a -= 1; b += 1;
                                        operacion[a] = Convert.ToString(resultado);
                                        operacion[j] = " "; operacion[b] = " ";
                                        j = a;
                                        organizar.buscaresp(pcdo, opera, operacion);
                                        acomodar.organiza(pcdo, opera, operacion);
                                        pcdo -= 2;
                                    }

                                }

                            }


                            if (opera >= 1)
                            {
                                k = Convert.ToByte(opera - 1);
                                if (operacion[k] == "+" || operacion[k] == "(" || operacion[k] == ")" || operacion[k] == "-" || operacion[k] == "*" || operacion[k] == "/")
                                {
                                    operacion[opera] = " "; operacion[pcdo] = " ";
                                    acomodar.organiza(pcdo, opera, operacion);

                                }
                                else
                                {
                                    operacion[opera] = "*"; operacion[pcdo] = " ";
                                    acomodar.organiza(pcdo, opera, operacion);
                                }
                            }


                            contar = 0;
                            for (int z = 0; z <= 19; z++)
                            {
                                if (operacion[z] == "(")
                                {
                                    contar++;
                                }
                            }

                            if (contar == 1) abierto = 1;

                        }
                    }
                }
            }

        }

    }

    class titulo
    {
        static void Main(string[] args)
        {
            Console.WriteLine("             Escribe una expresion Matemática \n ");
            Console.Title = ("Creado por: ----Taylor ");
            string[] operacion = new string[23];
            byte pos = 1, pfin = 0;
            string temp1, temp2 = " ";
            espacios enviar = new espacios();
            finalizado final = new finalizado();

            operacion[0] = "("; operacion[19] = ")";

            do
            {
                temp1 = Convert.ToString(Console.ReadKey().KeyChar);

                if (temp1 != "\r")
                {
                    if (temp2 == " ")
                    {

                        if (temp1 == "+" || temp1 == "(" || temp1 == ")" || temp1 == "-" || temp1 == "*" || temp1 == "/")
                        {
                            operacion[pos] = temp1;
                            pos++;

                        }
                        else
                        {
                            operacion[pos] = operacion[pos] + temp1;
                        }

                    }
                    else
                    {
                        if (temp1 == "+" || temp1 == "(" || temp1 == ")" || temp1 == "-" || temp1 == "*" || temp1 == "/")
                        {
                            if (temp2 == "+" || temp2 == "(" || temp2 == ")" || temp2 == "-" || temp2 == "*" || temp2 == "/")
                            {
                                operacion[pos] = temp1;
                                pos++;
                            }
                            else
                            {
                                pos++; operacion[pos] = temp1; pos++;
                            }

                        }
                        else
                        {
                            operacion[pos] = operacion[pos] + temp1;
                        }
                    }

                }
                else
                {
                    pfin = pos;
                }

                temp2 = Convert.ToString(Console.ReadKey().KeyChar);
                if (temp2 != "\r")
                {
                    if (temp2 == "+" || temp2 == "(" || temp2 == ")" || temp2 == "-" || temp2 == "*" || temp2 == "/")
                    {
                        if (temp1 == "+" || temp1 == "(" || temp1 == ")" || temp1 == "-" || temp1 == "*" || temp1 == "/")
                        {
                            operacion[pos] = temp2;
                            pos++;
                        }
                        else
                        {
                            pos++; operacion[pos] = temp2; pos++;
                        }

                    }
                    else
                    {
                        operacion[pos] = operacion[pos] + temp2;
                    }


                }
                else
                {
                    pfin = pos;
                }

            } while ((pos < 19) && (temp1 != "\r") && (temp2 != "\r"));

       


            enviar.parentesis(operacion, pfin);
            final.imprimir(operacion);

            Console.Clear();
            byte posx = 5;
            for (int m = 0; m <= 19; m++)
            {

                Console.SetCursorPosition(posx, 6); Console.WriteLine(operacion[m]);
                posx += 1;
            }

        }
    }
}

