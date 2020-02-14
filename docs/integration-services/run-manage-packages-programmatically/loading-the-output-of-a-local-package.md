---
title: Cargar la salida de un paquete local | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data flow [Integration Services], loading results
- loading data flow results
ms.assetid: aba8ecb7-0dcf-40d0-a2a8-64da0da94b93
author: chugugrace
ms.author: chugu
ms.openlocfilehash: dc35bb8b31c88cea2d903981e709f4075929ea7a
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "71295751"
---
# <a name="loading-the-output-of-a-local-package"></a>Cargar la salida de un paquete local

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Las aplicaciones cliente pueden leer la salida de los paquetes de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] cuando se guarda la salida en destinos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante [!INCLUDE[vstecado](../../includes/vstecado-md.md)] o cuando se guarda en un destino de archivo plano usando las clases del espacio de nombres **System.IO**. Sin embargo, una aplicación cliente también puede leer la salida de un paquete directamente de la memoria, sin tener que efectuar un paso intermedio para conservar los datos. La clave para esta solución es el espacio de nombres **Microsoft.SqlServer.Dts.DtsClient**, que contiene implementaciones especializadas de las interfaces **IDbConnection**, **IDbCommand** e **IDbDataParameter** del espacio de nombres **System.Data**. El ensamblado Microsoft.SqlServer.Dts.DtsClient.dll se instala de forma predeterminada en la carpeta **%Archivos de programa%\Microsoft SQL Server\100\DTS\Binn**.  

> [!IMPORTANT]
> El procedimiento descrito en este artículo, en el que se usa la biblioteca `DtsClient`, solo funciona en paquetes implementados con el modelo de implementación de paquetes (es decir, con la opción `/SQL`, `/DTS` o `/File`). Este procedimiento no funciona para los paquetes implementados con el modelo de implementación de servidor (es decir, con la opción `/ISServer`). Para consumir la salida de un paquete local implementado con el modelo de implementación de servidor (es decir, con la opción `/ISServer`), use el [Destino de streaming de datos](../data-flow/data-streaming-destination.md) en lugar del procedimiento descrito en este artículo.

> [!NOTE]  
> El procedimiento descrito en este tema necesita que la propiedad DelayValidation de la tarea Flujo de datos y de los objetos primarios esté establecida en el valor predeterminado de **False**.
  
## <a name="description"></a>Descripción  
 Este procedimiento muestra cómo desarrollar una aplicación cliente en código administrado que carga la salida de un paquete con un destino DataReader directamente de la memoria. Los pasos resumidos aquí se muestran en el ejemplo de código que figura a continuación.  
  
#### <a name="to-load-data-package-output-into-a-client-application"></a>Para cargar la salida del paquete de datos en una aplicación cliente  
  
1.  En el paquete, configure un destino DataReader para recibir la salida que desea leer en la aplicación cliente. Dé un nombre descriptivo al destino DataReader, dado que utilizará este nombre más adelante en la aplicación cliente. Tome nota del nombre del destino DataReader.  
  
2.  En el proyecto de desarrollo, para establecer una referencia al espacio de nombres **Microsoft.SqlServer.Dts.DtsClient**, ubique el ensamblado **Microsoft.SqlServer.Dts.DtsClient.dll**. De forma predeterminada, este ensamblado se instala en **C:\Archivos de programa\Microsoft SQL Server\100\DTS\Binn**. Importe el espacio de nombres en el código usando la instrucción **Using** o la instrucción [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] **Imports** de C#.  
  
3.  En el código, cree un objeto de tipo **DtsClient.DtsConnection** con una cadena de conexión que contenga los parámetros de línea de comandos que **dtexec.exe** necesita para ejecutar el paquete. Para obtener más información, consulte [utilidad dtexec](../../integration-services/packages/dtexec-utility.md). A continuación, abra la conexión con esta cadena de conexión. También puede emplear la utilidad **dtexecui** para crear visualmente la cadena de conexión necesaria.  
  
    > [!NOTE]  
    >  En el código de ejemplo se muestra cómo cargar el paquete del sistema de archivos mediante la sintaxis `/FILE <path and filename>`. No obstante, puede también cargar el paquete desde la base de datos MSDB utilizando la sintaxis `/SQL <package name>` o desde el almacén de paquetes de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] utilizando la sintaxis `/DTS \<folder name>\<package name>`.  
  
4.  Cree un objeto de tipo **DtsClient.DtsCommand** que utilice el objeto **DtsConnection** creado anteriormente y establezca la propiedad **CommandText** en el nombre del destino DataReader del paquete. A continuación, llame al método **ExecuteReader** del objeto de comando para cargar los resultados del paquete en un nuevo DataReader.  
  
5.  Opcionalmente, puede parametrizar indirectamente la salida del paquete utilizando la colección de objetos **DtsDataParameter** en el objeto **DtsCommand** para pasar los valores a las variables definidas en el paquete. Dentro del paquete, puede usar estas variables como parámetros de consulta o en expresiones para influir en los resultados devueltos al destino DataReader. Debe definir estas variables en el paquete del espacio de nombres **DtsClient** para poder usarlas con el objeto **DtsDataParameter** desde una aplicación cliente. (Quizá tenga que hacer clic en el botón de la barra de herramientas **Elegir columnas de variables** de la ventana **Variables** para mostrar la columna **Espacio de nombres**). En el código de cliente, al agregar **DtsDataParameter** a la colección **Parameters** de **DtsCommand**, omita la referencia al espacio de nombres DtsClient en el nombre de variable. Por ejemplo:  
  
    ```  
    command.Parameters.Add(new DtsDataParameter("MyVariable", 1));  
    ```  
  
6.  Llame al método **Read** de DataReader repetidamente según sea necesario para recorrer en bucle las filas de datos de salida. Utilice los datos, o guárdelos para un uso posterior, en la aplicación cliente.  
  
    > [!IMPORTANT]  
    >  El método **Read** de esta implementación de DataReader devuelve **true** una vez más después de leer la última fila de datos. Esto hace que sea difícil utilizar el código usual que recorre en bucle DataReader mientras **Read** devuelve **true**. Si el código intenta cerrar DataReader o la conexión después de leer el número esperado de filas, sin una llamada adicional y final al método **Read**, el código producirá una excepción no controlada. Sin embargo, si el código intenta leer los datos en esta última iteración a través de un bucle, cuando **Read** todavía devuelve **true** pero se ha pasado la última fila, el código producirá una excepción **ApplicationException** no controlada con el mensaje "IDataReader de SSIS se encuentra más allá del final del conjunto de resultados". Este comportamiento es distinto del que tienen otras implementaciones de DataReader. Por consiguiente, si utiliza un bucle para leer las filas de DataReader mientras **Read** devuelve **true**, tiene que escribir el código para capturar, probar y descartar esta excepción **ApplicationException** anticipada en la última llamada correcta al método **Read**. O bien, si conoce de antemano el número de filas esperado, puede procesar las filas y, a continuación, llamar al método **Read** una vez más antes de cerrar DataReader y la conexión.  
  
7.  Llame al método **Dispose** del objeto **DtsCommand**. Esto es particularmente importante si ha utilizado cualquier objeto **DtsDataParameter**.  
  
8.  Cierre DataReader y los objetos de conexión.  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente se ejecuta un paquete que calcula un valor de agregado único y guarda el valor en un destino DataReader y, a continuación, lee este valor de DataReader y muestra el valor en un cuadro de texto en un formulario Windows Forms.  
  
 No se requiere el uso de parámetros al cargar la salida de un paquete en una aplicación cliente. Si no desea usar un parámetro, puede omitir el uso de la variable en el espacio de nombres **DtsClient** y omitir el código que usa el objeto **DtsDataParameter**.  
  
#### <a name="to-create-the-test-package"></a>Para crear el paquete de prueba  
  
1.  Cree un nuevo paquete de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. En el código de ejemplo se utiliza "DtsClientWParamPkg.dtsx" como el nombre del paquete.  
  
2.  Agregue una variable de tipo String en el espacio de nombres DtsClient. En el ejemplo de código se usa Country como el nombre de la variable. (Quizá tenga que hacer clic en el botón de la barra de herramientas **Elegir columnas de variables** de la ventana **Variables** para mostrar la columna **Espacio de nombres**).  
  
3.  Agregue un administrador de conexiones OLE DB que se conecta a la base de datos de ejemplo [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)].  
  
4.  Agregue una tarea Flujo de datos al paquete y cambie a la superficie de diseño Flujo de datos.  
  
5.  Agregue un origen OLE DB al flujo de datos y configúrelo para utilizar el administrador de conexiones OLE DB creado anteriormente y el comando SQL siguiente:  
  
    ```  
    SELECT * FROM Sales.vIndividualCustomer WHERE CountryRegionName = ?  
    ```  
  
6.  Haga clic en **Parámetros** y, en el cuadro de diálogo **Establecer parámetros de consulta**, asigne el parámetro de entrada único de la consulta, Parameter0, a la variable DtsClient::Country.  
  
7.  Agregue una transformación Agregado al flujo de datos y conecte la salida del origen OLE DB a la transformación. Abra el Editor de transformación Agregado y configúrelo para realizar una operación "COUNT ALL" en todas las columnas de entrada (*) y generar el valor de agregado con el alias CustomerCount.  
  
8.  Agregue un destino DataReader al flujo de datos y conecte la salida de transformación Agregado al destino DataReader. En el código de ejemplo se utiliza "DataReaderDest" como el nombre del DataReader. Seleccione una columna de entrada disponible única, CustomerCount, para el destino.  
  
9. Guarde el paquete. La aplicación de prueba creada a continuación ejecutará el paquete y recuperará la salida directamente de la memoria.  
  
#### <a name="to-create-the-test-application"></a>Para crear la aplicación de prueba  
  
1.  Cree una nueva aplicación Windows Forms.  
  
2.  Para agregar una referencia al espacio de nombres **Microsoft.SqlServer.Dts.DtsClient**, navegue hasta el ensamblado con el mismo nombre en la carpeta **%Archivos de programa%\Microsoft SQL Server\100\DTS\Binn**.  
  
3.  Copie y pegue el código muestra siguiente en el módulo de código del formulario.  
  
4.  Modifique el valor de la variable **dtexecArgs** según sea necesario para que contenga los parámetros de línea de comandos necesarios para que **dtexec.exe** ejecute el paquete. En el código muestra se carga el paquete desde el sistema de archivos.  
  
5.  Modifique el valor de la variable **dataReaderName** según sea necesario para que contenga el nombre del destino DataReader del paquete.  
  
6.  Coloque un botón y un cuadro de texto en el formulario. En el código de ejemplo se utiliza **btnRun** como el nombre del botón y **txtResults** como el nombre del cuadro de texto.  
  
7.  Ejecute la aplicación y haga clic en el botón. Después de una breve pausa mientras el paquete se ejecuta, debería aparecer en el cuadro de texto del formulario el valor agregado calculado por el paquete (el recuento de clientes de Canadá).  
  
### <a name="sample-code"></a>Código de ejemplo  
  
```vb  
Imports System.Data  
Imports Microsoft.SqlServer.Dts.DtsClient  
  
Public Class Form1  
  
  Private Sub btnRun_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles btnRun.Click  
  
    Dim dtexecArgs As String  
    Dim dataReaderName As String  
    Dim countryName As String  
  
    Dim dtsConnection As DtsConnection  
    Dim dtsCommand As DtsCommand  
    Dim dtsDataReader As IDataReader  
    Dim dtsParameter As DtsDataParameter  
  
    Windows.Forms.Cursor.Current = Cursors.WaitCursor  
  
    dtexecArgs = "/FILE ""C:\...\DtsClientWParamPkg.dtsx"""  
    dataReaderName = "DataReaderDest"  
    countryName = "Canada"  
  
    dtsConnection = New DtsConnection()  
    With dtsConnection  
      .ConnectionString = dtexecArgs  
      .Open()  
    End With  
  
    dtsCommand = New DtsCommand(dtsConnection)  
    dtsCommand.CommandText = dataReaderName  
  
    dtsParameter = New DtsDataParameter("Country", DbType.String)  
    dtsParameter.Direction = ParameterDirection.Input  
    dtsCommand.Parameters.Add(dtsParameter)  
  
    dtsParameter.Value = countryName  
  
    dtsDataReader = dtsCommand.ExecuteReader(CommandBehavior.Default)  
  
    With dtsDataReader  
      .Read()  
      txtResults.Text = .GetInt32(0).ToString("N0")  
    End With  
  
    'After reaching the end of data rows,  
    ' call the Read method one more time.  
    Try  
      dtsDataReader.Read()  
    Catch ex As Exception  
      MessageBox.Show("Exception on final call to Read method:" & ControlChars.CrLf & _  
      ex.Message & ControlChars.CrLf & _  
      ex.InnerException.Message, "Exception on final call to Read method", _  
      MessageBoxButtons.OK, MessageBoxIcon.Error)  
    End Try  
  
    ' The following method is a best practice, and is  
    '  required when using DtsDataParameter objects.  
    dtsCommand.Dispose()  
  
    Try  
      dtsDataReader.Close()  
    Catch ex As Exception  
      MessageBox.Show("Exception closing DataReader:" & ControlChars.CrLf & _  
      ex.Message & ControlChars.CrLf & _  
      ex.InnerException.Message, "Exception closing DataReader", _  
      MessageBoxButtons.OK, MessageBoxIcon.Error)  
    End Try  
  
    Try  
      dtsConnection.Close()  
    Catch ex As Exception  
      MessageBox.Show("Exception closing connection:" & ControlChars.CrLf & _  
      ex.Message & ControlChars.CrLf & _  
      ex.InnerException.Message, "Exception closing connection", _  
      MessageBoxButtons.OK, MessageBoxIcon.Error)  
    End Try  
  
    Windows.Forms.Cursor.Current = Cursors.Default  
  
  End Sub  
  
End Class  
```  
  
```csharp  
using System;  
using System.Windows.Forms;  
using System.Data;  
using Microsoft.SqlServer.Dts.DtsClient;  
  
namespace DtsClientWParamCS  
{  
  public partial class Form1 : Form  
  {  
    public Form1()  
    {  
      InitializeComponent();  
      this.btnRun.Click += new System.EventHandler(this.btnRun_Click);  
    }  
  
    private void btnRun_Click(object sender, EventArgs e)  
    {  
      string dtexecArgs;  
      string dataReaderName;  
      string countryName;  
  
      DtsConnection dtsConnection;  
      DtsCommand dtsCommand;  
      IDataReader dtsDataReader;  
      DtsDataParameter dtsParameter;  
  
      Cursor.Current = Cursors.WaitCursor;  
  
      dtexecArgs = @"/FILE ""C:\...\DtsClientWParamPkg.dtsx""";  
      dataReaderName = "DataReaderDest";  
      countryName = "Canada";  
  
      dtsConnection = new DtsConnection();  
      {  
        dtsConnection.ConnectionString = dtexecArgs;  
        dtsConnection.Open();  
      }  
  
      dtsCommand = new DtsCommand(dtsConnection);  
      dtsCommand.CommandText = dataReaderName;  
  
      dtsParameter = new DtsDataParameter("Country", DbType.String);  
      dtsParameter.Direction = ParameterDirection.Input;  
      dtsCommand.Parameters.Add(dtsParameter);  
  
      dtsParameter.Value = countryName;  
  
      dtsDataReader = dtsCommand.ExecuteReader(CommandBehavior.Default);  
  
      {  
        dtsDataReader.Read();  
        txtResults.Text = dtsDataReader.GetInt32(0).ToString("N0");  
      }  
  
      //After reaching the end of data rows,  
      // call the Read method one more time.  
      try  
      {  
        dtsDataReader.Read();  
      }  
      catch (Exception ex)  
      {  
        MessageBox.Show(  
          "Exception on final call to Read method:\n" + ex.Message + "\n" + ex.InnerException.Message,  
          "Exception on final call to Read method", MessageBoxButtons.OK, MessageBoxIcon.Error);  
      }  
  
      // The following method is a best practice, and is  
      //  required when using DtsDataParameter objects.  
      dtsCommand.Dispose();  
  
      try  
      {  
        dtsDataReader.Close();  
      }  
      catch (Exception ex)  
      {  
        MessageBox.Show(  
          "Exception closing DataReader:\n" + ex.Message + "\n" + ex.InnerException.Message,  
          "Exception closing DataReader", MessageBoxButtons.OK, MessageBoxIcon.Error);  
      }  
  
      try  
      {  
        dtsConnection.Close();  
      }  
      catch (Exception ex)  
      {  
        MessageBox.Show(  
          "Exception closing connection:\n" + ex.Message + "\n" + ex.InnerException.Message,  
          "Exception closing connection", MessageBoxButtons.OK, MessageBoxIcon.Error);  
      }  
  
      Cursor.Current = Cursors.Default;  
  
    }  
  }  
}  
```  
  
## <a name="see-also"></a>Consulte también  
 [Descripción de las diferencias entre la ejecución local y remota](../../integration-services/run-manage-packages-programmatically/understanding-the-differences-between-local-and-remote-execution.md)   
 [Cargar y ejecutar un paquete local mediante programación](../../integration-services/run-manage-packages-programmatically/loading-and-running-a-local-package-programmatically.md)   
 [Cargar y ejecutar un paquete remoto mediante programación](../../integration-services/run-manage-packages-programmatically/loading-and-running-a-remote-package-programmatically.md)  
  
  
