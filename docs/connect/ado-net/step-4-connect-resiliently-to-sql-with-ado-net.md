---
title: 'Paso 4: Conexión resistente a SQL con ADO.NET | Microsoft Docs'
ms.custom: ''
ms.date: 08/08/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
dev_langs:
- CSharp
ms.assetid: 9b608b0b-6b38-42da-bb83-79df8c170cd7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9a812aacbbbd87ba8fc38479be7d62a0fc9401b6
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47731373"
---
# <a name="step-4-connect-resiliently-to-sql-with-adonet"></a>Paso 4: Conectar la resistencia a SQL con ADO.NET

- Artículo anterior:&nbsp;&nbsp;&nbsp;[Paso 3: Prueba de concepto de la conexión a SQL mediante ADO.NET](step-3-proof-of-concept-connecting-to-sql-using-ado-net.md)  

  
En este tema se proporciona un ejemplo de código C# que muestra la lógica de reintento personalizada. La lógica de reintento proporciona confiabilidad. La lógica de reintento está diseñada para procesar correctamente los errores temporales o *errores transitorios* que tienden a desaparecer si el programa espera varios segundos y vuelve a intentarlo.  
  
Los orígenes de errores transitorios incluyen:  
  
- Un error breve de las funciones de red que es compatible con Internet.  
- Un sistema en la nube podría ser el equilibrio de carga sus recursos en el momento en que se envió la consulta.  
  
  
Las clases de ADO.NET para conectarse a Microsoft SQL Server local también pueden conectarse a Azure SQL Database. Sin embargo, por sí mismos ADO.NET clases no pueden proporcionar la solidez y confiabilidad necesarias en su uso en producción. El programa cliente puede detectar errores transitorios del que se debe forma silenciosa y sencilla recuperarse y continuar por sí mismo.  
  
## <a name="step-1-identify-transient-errors"></a>Paso 1: Identificar los errores transitorios  
  
El programa debe distinguir entre errores transitorios frente a errores persistentes. Errores transitorios son las condiciones de error que se pueden borrar en un breve período de tiempo, como problemas de red transitorios.  Un ejemplo de un error persistente sería si el programa tiene un error ortográfico en el nombre de la base de datos de destino: en este caso, debería conservar el error "No dicha base de datos que se encuentra" y no tiene ninguna posibilidad de borrar en un breve período de tiempo.  
  
Está disponible en la lista de números de error que se clasifican como errores transitorios [mensajes de Error para las aplicaciones de cliente de base de datos SQL](http://docs.microsoft.com/azure/sql-database/sql-database-develop-error-messages/)  
  
## <a name="step-2-create-and-run-sample-application"></a>Paso 2: Crear y ejecutar la aplicación de ejemplo  
  
En este ejemplo se da por supuesto .NET Framework 4.5.1 o posterior está instalado.  El ejemplo de código de C# consta de un archivo denominado Program.cs. Su código se proporciona en la sección siguiente.  
  
### <a name="step-2a-capture-and-compile-the-code-sample"></a>Paso 2.a: capturar y compile el ejemplo de código  
  
Puede compilar el ejemplo con los pasos siguientes:  
  
1. En el [edición gratuita Visual Studio Community](https://www.visualstudio.com/products/visual-studio-community-vs), cree un nuevo proyecto a partir de la plantilla de aplicación de consola C#.  
    - Archivo > Nuevo > proyecto > instalado > Plantillas > Visual C# > Windows > escritorio clásico > aplicación de consola  
    - Denomine el proyecto **RetryAdo2**.  
2. Abra el panel Explorador de soluciones.  
    - Ver el nombre del proyecto.  
    - Ver el nombre del archivo Program.cs.  
3. Abra el archivo Program.cs.  
4. Reemplazar completamente el contenido del archivo Program.cs con el código en el bloque de código siguiente.  
5. Haga clic en el menú compilar > compilar solución.  
  
### <a name="step-2b-copy-and-paste-sample-code"></a>Paso 2.b: copiar y pegar código de ejemplo  
  
Pegue este código en su **Program.cs** archivo.  
  
A continuación, debe editar las cadenas de nombre de servidor, contraseña y así sucesivamente. Puede encontrar estas cadenas en el método llamado **GetSqlConnectionStringBuilder**.  
  
Nota: La cadena de conexión para el nombre del servidor está orientada a la base de datos de SQL Azure, ya que incluye el prefijo de cuatro caracteres de **tcp:**. Pero puede ajustar la cadena de servidor para conectarse a Microsoft SQL Server.  
  
  
```CSharp  
    using System;  // C#  
    using CG = System.Collections.Generic;  
    using QC = System.Data.SqlClient;  
    using TD = System.Threading;  
        
    namespace RetryAdo2  
    {  
      public class Program  
      {  
        static public int Main(string[] args)  
        {  
          bool succeeded = false;  
          int totalNumberOfTimesToTry = 4;  
          int retryIntervalSeconds = 10;  
        
          for (int tries = 1;  
            tries <= totalNumberOfTimesToTry;  
            tries++)  
          {  
            try  
            {  
              if (tries > 1)  
              {  
                Console.WriteLine  
                  ("Transient error encountered. Will begin attempt number {0} of {1} max...",  
                  tries, totalNumberOfTimesToTry  
                  );  
                TD.Thread.Sleep(1000 * retryIntervalSeconds);  
                retryIntervalSeconds = Convert.ToInt32  
                  (retryIntervalSeconds * 1.5);  
              }  
              AccessDatabase();  
              succeeded = true;  
              break;  
            }  
        
            catch (QC.SqlException sqlExc)  
            {  
              if (TransientErrorNumbers.Contains  
                (sqlExc.Number) == true)  
              {  
                Console.WriteLine("{0}: transient occurred.", sqlExc.Number);  
                continue;  
              }  
              else  
              {  
                Console.WriteLine(sqlExc);  
                succeeded = false;  
                break;  
              }  
            }  
        
            catch (TestSqlException sqlExc)  
            {  
              if (TransientErrorNumbers.Contains  
                (sqlExc.Number) == true)  
              {  
                Console.WriteLine("{0}: transient occurred. (TESTING.)", sqlExc.Number);  
                continue;  
              }  
              else  
              {  
                Console.WriteLine(sqlExc);  
                succeeded = false;  
                break;  
              }  
            }  
        
            catch (Exception Exc)  
            {  
              Console.WriteLine(Exc);  
              succeeded = false;  
              break;  
            }  
          }  
        
          if (succeeded == true)  
          {  
            return 0;  
          }  
          else  
          {  
            Console.WriteLine("ERROR: Unable to access the database!");  
            return 1;  
          }  
        }  
        
        /// <summary>  
        /// Connects to the database, reads,  
        /// prints results to the console.  
        /// </summary>  
        static public void AccessDatabase()  
        {  
          //throw new TestSqlException(4060); //(7654321);  // Uncomment for testing.  
        
          using (var sqlConnection = new QC.SqlConnection  
              (GetSqlConnectionString()))  
          {  
            using (var dbCommand = sqlConnection.CreateCommand())  
            {  
              dbCommand.CommandText = @"  
    SELECT TOP 3  
        ob.name,  
        CAST(ob.object_id as nvarchar(32)) as [object_id]  
      FROM sys.objects as ob  
      WHERE ob.type='IT'  
      ORDER BY ob.name;";  
        
              sqlConnection.Open();  
              var dataReader = dbCommand.ExecuteReader();  
        
              while (dataReader.Read())  
              {  
                Console.WriteLine("{0}\t{1}",  
                  dataReader.GetString(0),  
                  dataReader.GetString(1));  
              }  
            }  
          }  
        }  
        
        /// <summary>  
        /// You must edit the four 'my' string values.  
        /// </summary>  
        /// <returns>An ADO.NET connection string.</returns>  
        static private string GetSqlConnectionString()  
        {  
          // Prepare the connection string to Azure SQL Database.  
          var sqlConnectionSB = new QC.SqlConnectionStringBuilder();  
        
          // Change these values to your values.  
          sqlConnectionSB.DataSource = "tcp:myazuresqldbserver.database.windows.net,1433"; //["Server"]  
          sqlConnectionSB.InitialCatalog = "MyDatabase"; //["Database"]  
        
          sqlConnectionSB.UserID = "MyLogin";  // "@yourservername"  as suffix sometimes.  
          sqlConnectionSB.Password = "MyPassword";  
          sqlConnectionSB.IntegratedSecurity = false;  
        
          // Adjust these values if you like. (ADO.NET 4.5.1 or later.)  
          sqlConnectionSB.ConnectRetryCount = 3;  
          sqlConnectionSB.ConnectRetryInterval = 10;  // Seconds.  
        
          // Leave these values as they are.  
          sqlConnectionSB.IntegratedSecurity = false;  
          sqlConnectionSB.Encrypt = true;  
          sqlConnectionSB.ConnectTimeout = 30;  
        
          return sqlConnectionSB.ToString();  
        }  
        
        static public CG.List<int> TransientErrorNumbers =  
          new CG.List<int> { 4060, 40197, 40501, 40613,  
          49918, 49919, 49920, 11001 };  
      }  
        
      /// <summary>  
      /// For testing retry logic, you can have method  
      /// AccessDatabase start by throwing a new  
      /// TestSqlException with a Number that does  
      /// or does not match a transient error number  
      /// present in TransientErrorNumbers.  
      /// </summary>  
      internal class TestSqlException : ApplicationException  
      {  
        internal TestSqlException(int testErrorNumber)  
        { this.Number = testErrorNumber; }  
        
        internal int Number  
        { get; set; }  
      }  
    }  
```  
  
###  <a name="step-2c-run-the-program"></a>Paso 2.c: ejecutar el programa  
  
  
El **RetryAdo2.exe** ejecutable no entradas parámetros. Para ejecutar el archivo .exe:  
  
1. Abra una ventana de la consola donde haya compilado el binario RetryAdo2.exe.  
2. Ejecute RetryAdo2.exe sin parámetros de entrada.  
  
  
  
```  
    database_firewall_rules_table   245575913  
    filestream_tombstone_2073058421 2073058421  
    filetable_updates_2105058535    2105058535  
```  
  
  
  
## <a name="step-3-ways-to-test-your-retry-logic"></a>Paso 3: Formas de probar la lógica de reintento  
  
Hay una gran variedad de formas puede simular un error transitorio para probar la lógica de reintento.  
  
  
###  <a name="step-3a-throw-a-test-exception"></a>Paso 3.a: producir una excepción de prueba  
  
El ejemplo de código incluye:  
  
- Una segunda clase pequeña denominada **TestSqlException**, con una propiedad denominada **número**.  
- `//throw new TestSqlException(4060);` , que puede quitar el comentario.  
  
Si quita los comentarios de la instrucción throw y vuelva a compilar, la siguiente ejecución de **RetryAdo2.exe** genera algo parecido a lo siguiente.  
  
```  
    [C:\VS15\RetryAdo2\RetryAdo2\bin\Debug\]  
    >> RetryAdo2.exe  
    4060: transient occurred. (TESTING.)  
    Transient error encountered. Will begin attempt number 2 of 4 max...  
    4060: transient occurred. (TESTING.)  
    Transient error encountered. Will begin attempt number 3 of 4 max...  
    4060: transient occurred. (TESTING.)  
    Transient error encountered. Will begin attempt number 4 of 4 max...  
    4060: transient occurred. (TESTING.)  
    ERROR: Unable to access the database!  
      
    [C:\VS15\RetryAdo2\RetryAdo2\bin\Debug\]  
    >>  
```  
  
###  <a name="step-3b-retest-with-a-persistent-error"></a>El paso 3.b: volver a probar con un error persistente  
  
Para demostrar que el código controla errores persistentes correctamente, vuelva a ejecutar la prueba anterior no utilizar el número de un error transitorio real como 4060. En su lugar, use el número sin sentido 7654321. El programa debería tratarlo como un error persistente y omitir cualquier reintento.  
  
###  <a name="step-3c-disconnect-from-the-network"></a>Paso 3.c: desconectar de la red  
  
1. Desconecte el equipo cliente de la red.  
    - Para un equipo de escritorio, desconecte el cable de red.  
    - Para un equipo portátil, presione la combinación de teclas para desactivar el adaptador de red de la función.  
2. Inicie RetryAdo2.exe y espere a que la consola mostrar el primer error transitorio, probablemente 11001.  
3. Volver a conectarse a la red mientras RetryAdo2.exe continúa ejecutándose.  
4. Ver el éxito de informe de la consola en un reintento posterior.  
  
  
###  <a name="step-2d-temporarily-misspell-the-server-name"></a>Paso 2.d: escribir mal temporalmente el nombre del servidor  
  
1. Agregue temporalmente 40615 como otro número de error a **TransientErrorNumbers**y vuelva a compilar.  
2. Establezca un punto de interrupción en la línea: `new QC.SqlConnectionStringBuilder()`.  
3. Use la *editar y continuar* característica para escribir mal deliberadamente el nombre del servidor, un par de líneas por debajo.  
    - Permitir que el programa ejecute y vuelva a su punto de interrupción.  
    - Se produce el error 40615.  
4. Corrija el error ortográfico.  
5. Deje que el programa se ejecutan y completan correctamente.  
6. Quite 40615 y vuelva a compilar.  
  
## <a name="next-steps"></a>Next Steps  
  
Para explorar otros practicies recomendadas y directrices de diseño, visite [conectarse a SQL Database: vínculos, prácticas recomendadas y directrices de diseño](http://azure.microsoft.com/documentation/articles/sql-database-connect-central-recommendations/)  
