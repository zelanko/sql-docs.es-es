---
title: 'Paso 4: conexión resistente a SQL con ADO.NET | Microsoft Docs'
description: Describe cómo conectar reciliently a SQL
ms.custom: ''
ms.date: 08/15/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: rothja
ms.technology: connectivity
ms.topic: conceptual
dev_langs:
- CSharp
ms.assetid: 9b608b0b-6b38-42da-bb83-79df8c170cd7
author: v-kaywon
ms.author: v-kaywon
ms.openlocfilehash: 62ec2eb775ef5fba76b402d1871afe6c87bcc606
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 10/16/2019
ms.locfileid: "72451802"
---
# <a name="step-4-connect-resiliently-to-sql-with-adonet"></a>Paso 4: Conectar la resistencia a SQL con ADO.NET

![Download-DownArrow-Circled](../../ssdt/media/download.png)[Descargar ADO.NET](../sql-connection-libraries.md#anchor-20-drivers-relational-access)

- Artículo anterior:&nbsp;&nbsp;&nbsp;[Paso 3: Prueba de concepto de la conexión a SQL mediante ADO.NET](step-3-connect-sql-ado-net.md)  

  
Este tema brinda un ejemplo de código C# que muestra lógica de reintento personalizada. La lógica de reintento ofrece confiabilidad. La lógica de reintento está diseñada para procesar correctamente los errores temporales o los errores *transitorios* que tienden a desaparecer si el programa espera varios segundos y reintentos.  
  
Los orígenes de errores transitorios incluyen:  
  
- Un breve error de las redes que admite Internet.  
- Un sistema en la nube podría estar equilibrando la carga de sus recursos en el momento en que se envió la consulta.  
  
  
Las clases ADO.NET para conectarse al servidor Microsoft SQL Server local también se pueden conectar a Azure SQL Database. Sin embargo, las clases ADO.NET no pueden proporcionar toda la robustez y la confiabilidad necesarias en el uso de producción. El programa cliente puede encontrar errores transitorios de los que debe recuperarse de forma silenciosa y correcta y continuar por sí solo.  
  
## <a name="step-1-identify-transient-errors"></a>Paso 1: identificación de errores transitorios  
  
El programa debe distinguir entre errores transitorios frente a errores persistentes. Los errores transitorios son condiciones de error que pueden borrarse en un breve período de tiempo, como problemas de red transitorios.  Un ejemplo de un error persistente sería si el programa tiene un error ortográfico en el nombre de la base de datos de destino; en este caso, el error "no se encontró esa base de datos" se conservaría y no tiene la posibilidad de borrar en un breve período de tiempo.  
  
La lista de números de error que se clasifican como errores transitorios está disponible en [los mensajes de error de las aplicaciones cliente de SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-develop-error-messages/)  
  
## <a name="step-2-create-and-run-sample-application"></a>Paso 2: crear y ejecutar una aplicación de ejemplo  
  
En este ejemplo se asume que se ha instalado .NET Framework 4.5.1 o posterior.  El C# ejemplo de código se compone de un archivo denominado Program.cs. Su código se proporciona en la sección siguiente.  
  
### <a name="step-2a-capture-and-compile-the-code-sample"></a>Paso 2. a: capturar y compilar el ejemplo de código  
  
Puede compilar el ejemplo con los pasos siguientes:  
  
1. En la [edición gratuita de Visual Studio Community](https://www.visualstudio.com/products/visual-studio-community-vs), cree un nuevo proyecto a C# partir de la plantilla aplicación de consola.  
    - Archivo > nuevo proyecto de > > instalado > Plantillas > C# aplicación de consola > de escritorio clásico de Windows > visual >  
    - Asigne al proyecto el nombre **RetryAdo2**.  
2. Abra el panel Explorador de soluciones.  
    - Vea el nombre del proyecto.  
    - Vea el nombre del archivo Program.cs.  
3. Abra el archivo Program.cs.  
4. Reemplace por completo el contenido del archivo Program.cs por el código del siguiente bloque de código.  
5. Haga clic en el menú compilar > compilar solución.  
  
### <a name="step-2b-copy-and-paste-sample-code"></a>Paso 2. b: copiar y pegar el código de ejemplo  
  
Pegue este código en el archivo **Program.CS** .  
  
A continuación, debe modificar las cadenas para el nombre del servidor, la contraseña, etc. Puede encontrar estas cadenas en el método denominado **GetSqlConnectionStringBuilder**.  
  
Nota: la cadena de conexión para el nombre del servidor está orientada hacia Azure SQL Database, porque incluye el prefijo de cuatro caracteres de **TCP:** . Sin embargo, puede ajustar la cadena de servidor para conectarse a su Microsoft SQL Server.  
  
  
```csharp
using System;  // C#  
using CG = System.Collections.Generic;  
using QC = Microsoft.Data.SqlClient;  
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
  
###  <a name="step-2c-run-the-program"></a>Paso 2. c: ejecutar el programa  
  
  
El ejecutable **RetryAdo2. exe** no escribe ningún parámetro. Para ejecutar el archivo. exe:  
  
1. Abra una ventana de consola donde haya compilado el archivo binario RetryAdo2. exe.  
2. Ejecute RetryAdo2. exe sin parámetros de entrada.  
  
  
  
```  
database_firewall_rules_table   245575913  
filestream_tombstone_2073058421 2073058421  
filetable_updates_2105058535    2105058535  
```  
  
  
  
## <a name="step-3-ways-to-test-your-retry-logic"></a>Paso 3: formas de probar la lógica de reintento  
  
Hay varias maneras de simular un error transitorio para probar la lógica de reintento.  
  
  
###  <a name="step-3a-throw-a-test-exception"></a>Paso 3. a: iniciar una excepción de prueba  
  
El ejemplo de código incluye:  
  
- Una segunda clase pequeña denominada **TestSqlException**, con una propiedad denominada **Number**.  
- `//throw new TestSqlException(4060);`, que puede quitar de comentario.  
  
Si quita la marca de comentario de la instrucción throw y vuelve a compilar, la siguiente ejecución de **RetryAdo2. exe** genera algo parecido a lo siguiente.  
  
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
  
###  <a name="step-3b-retest-with-a-persistent-error"></a>Paso 3. b: reprueba con un error persistente  
  
Para demostrar que el código controla los errores persistentes correctamente, vuelva a ejecutar la prueba anterior, excepto no use el número de un error transitorio real como 4060. En su lugar, use el número que no sea 7654321. El programa debe tratarlo como un error persistente y debe omitir cualquier reintento.  
  
###  <a name="step-3c-disconnect-from-the-network"></a>Paso 3. c: desconexión de la red  
  
1. Desconecte el equipo cliente de la red.  
    - Para un escritorio, desconecte el cable de red.  
    - Para un equipo portátil, presione la combinación de funciones de teclas para desactivar el adaptador de red.  
2. Inicie RetryAdo2. exe y espere a que la consola muestre el primer error transitorio, probablemente 11001.  
3. Vuelva a conectarse a la red, mientras que RetryAdo2. exe continúa ejecutándose.  
4. Observe que el informe de la consola se realizó correctamente en un reintento posterior.  
  
  
###  <a name="step-2d-temporarily-misspell-the-server-name"></a>Paso 2. d: deletrear temporalmente el nombre del servidor  
  
1. Agregue temporalmente 40615 como otro número de error a **TransientErrorNumbers**y vuelva a compilar.  
2. Establezca un punto de interrupción en la línea: `new QC.SqlConnectionStringBuilder()`.  
3. Use la característica *Editar y continuar* para escribir incorrectamente el nombre del servidor, un par de líneas a continuación.  
    - Deje que el programa se ejecute y vuelva al punto de interrupción.  
    - Se produce el error 40615.  
4. Corrija la ortografía.  
5. Permita que el programa se ejecute y finalice correctamente.  
6. Quite 40615 y vuelva a compilar.  
  
## <a name="next-steps"></a>Pasos siguientes  
  
Para explorar otras prácticas recomendadas y directrices de diseño, visite [conexión a SQL Database: vínculos, prácticas recomendadas y directrices de diseño](https://azure.microsoft.com/documentation/articles/sql-database-connect-central-recommendations/)  
