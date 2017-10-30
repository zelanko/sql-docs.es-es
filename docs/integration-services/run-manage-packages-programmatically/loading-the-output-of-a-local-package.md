---
title: Cargar la salida de un paquete Local | Documentos de Microsoft
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data flow [Integration Services], loading results
- loading data flow results
ms.assetid: aba8ecb7-0dcf-40d0-a2a8-64da0da94b93
caps.latest.revision: 66
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 41de742c987d9f043f3dd247ee84af6a3eaf365b
ms.contentlocale: es-es
ms.lasthandoff: 09/26/2017

---
# <a name="loading-the-output-of-a-local-package"></a>Cargar la salida de un paquete local
  Las aplicaciones cliente pueden leer la salida de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] paquetes cuando se guarda el resultado en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] destinos mediante el uso de [!INCLUDE[vstecado](../../includes/vstecado-md.md)], o cuando se guarda la salida a un destino de archivo sin formato mediante el uso de las clases en el **System.IO** espacio de nombres. Sin embargo, una aplicación cliente también puede leer la salida de un paquete directamente de la memoria, sin tener que efectuar un paso intermedio para conservar los datos. La clave para esta solución es la **Microsoft.SqlServer.Dts.DtsClient** espacio de nombres, que contiene implementaciones especializadas de los **IDbConnection**, **IDbCommand**, y **IDbDataParameter** interfaces de la **System.Data** espacio de nombres. El ensamblado Microsoft.SqlServer.Dts.DtsClient.dll se instala de forma predeterminada en **%ProgramFiles%\Microsoft SQL Server\100\DTS\Binn**.  
  
> [!NOTE]  
>  El procedimiento descrito en este tema requiere que se establece la propiedad DelayValidation de la tarea flujo de datos y de los objetos primarios en su valor predeterminado de **False**.  
  
## <a name="description"></a>Description  
 Este procedimiento muestra cómo desarrollar una aplicación cliente en código administrado que carga la salida de un paquete con un destino DataReader directamente de la memoria. Los pasos resumidos aquí se muestran en el ejemplo de código que figura a continuación.  
  
#### <a name="to-load-data-package-output-into-a-client-application"></a>Para cargar la salida del paquete de datos en una aplicación cliente  
  
1.  En el paquete, configure un destino DataReader para recibir la salida que desea leer en la aplicación cliente. Dé un nombre descriptivo al destino DataReader, dado que utilizará este nombre más adelante en la aplicación cliente. Tome nota del nombre del destino DataReader.  
  
2.  En el proyecto de desarrollo, establezca una referencia la **Microsoft.SqlServer.Dts.DtsClient** espacio de nombres ubicando el ensamblado **Microsoft.SqlServer.Dts.DtsClient.dll**. De forma predeterminada, este ensamblado se instala en **C:\Program Files\Microsoft SQL Server\100\DTS\Binn**. Importa el espacio de nombres en el código mediante el uso de C# **mediante** o [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] **importaciones** instrucción.  
  
3.  En el código, cree un objeto de tipo **DtsClient.DtsConnection** con una cadena de conexión que contiene los parámetros de línea de comandos requeridos por **dtexec.exe** para ejecutar el paquete. Para más información, consulte [dtexec Utility](../../integration-services/packages/dtexec-utility.md). A continuación, abra la conexión con esta cadena de conexión. También puede usar el **dtexecui** utilidad para crear visualmente la cadena de conexión necesaria.  
  
    > [!NOTE]  
    >  En el código de ejemplo se muestra cómo cargar el paquete del sistema de archivos mediante la sintaxis `/FILE <path and filename>`. No obstante, puede también cargar el paquete desde la base de datos MSDB utilizando la sintaxis `/SQL <package name>` o desde el almacén de paquetes de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] utilizando la sintaxis `/DTS \<folder name>\<package name>`.  
  
4.  Crear un objeto de tipo **DtsClient.DtsCommand** que usa creado previamente **DtsConnection** y establecer su **CommandText** propiedad con el nombre del DataReader destino del paquete. A continuación, llame a la **ExecuteReader** método del objeto de comando para cargar los resultados del paquete en un nuevo DataReader.  
  
5.  Si lo desea, puede parametrizar indirectamente la salida del paquete mediante el uso de la colección de **DtsDataParameter** objetos en el **DtsCommand** objeto para pasar valores a las variables definidas en el paquete. Dentro del paquete, puede usar estas variables como parámetros de consulta o en expresiones para influir en los resultados devueltos al destino DataReader. Debe definir estas variables en el paquete en el **DtsClient** espacio de nombres antes de poder usarlas con el **DtsDataParameter** objeto desde una aplicación cliente. (Puede que necesite haga clic en el **Elegir columnas de variables** botón de barra de herramientas en el **Variables** ventana para mostrar la **Namespace** columna.) En el código de cliente, cuando se agrega un **DtsDataParameter** a la **parámetros** colección de la **DtsCommand**, omitir la referencia al espacio de nombres DtsClient desde el nombre de variable . Por ejemplo:  
  
    ```  
    command.Parameters.Add(new DtsDataParameter("MyVariable", 1));  
    ```  
  
6.  Llame a la **lectura** método de DataReader repetidamente según sea necesario para recorrer las filas de los datos de salida. Utilice los datos, o guárdelos para un uso posterior, en la aplicación cliente.  
  
    > [!IMPORTANT]  
    >  El **lectura** método de esta implementación de DataReader devuelve **true** otra vez después de que se ha leído la última fila de datos. Esto resulta difícil de usar el código usual que recorre en bucle DataReader mientras **lectura** devuelve **true**. Si el código intenta cerrar DataReader o la conexión después de leer el número esperado de filas, sin una llamada adicional, final a la **lectura** método, el código producirá una excepción no controlada. Sin embargo, si el código intenta leer los datos en esta última iteración a través de un bucle, cuando **lectura** sigue devolviendo **true** pero se ha pasado la última fila, el código producirá una no controlada  **ApplicationException** con el mensaje, "IDataReader de SSIS está más allá del final del conjunto de resultados". Este comportamiento es distinto del que tienen otras implementaciones de DataReader. Por lo tanto, cuando se usa un bucle para leer las filas de DataReader mientras **lectura** devuelve **true**, necesita escribir código para capturar, probar y descartar esta prever  **ApplicationException** en la última llamada correcta a la **lectura** método. O bien, si sabe de antemano el número de filas esperado, puede procesar las filas y, a continuación, llame a la **lectura** método una vez más antes de cerrar DataReader y la conexión.  
  
7.  Llame a la **Dispose** método de la **DtsCommand** objeto. Esto es especialmente importante si ha utilizado cualquier **DtsDataParameter** objetos.  
  
8.  Cierre DataReader y los objetos de conexión.  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente se ejecuta un paquete que calcula un valor de agregado único y guarda el valor en un destino DataReader y, a continuación, lee este valor de DataReader y muestra el valor en un cuadro de texto en un formulario Windows Forms.  
  
 No se requiere el uso de parámetros al cargar la salida de un paquete en una aplicación cliente. Si no desea usar un parámetro, puede omitir el uso de la variable en el **DtsClient** espacio de nombres y se omite el código que usa el **DtsDataParameter** objeto.  
  
#### <a name="to-create-the-test-package"></a>Para crear el paquete de prueba  
  
1.  Cree un nuevo paquete de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. En el código de ejemplo se utiliza "DtsClientWParamPkg.dtsx" como el nombre del paquete.  
  
2.  Agregue una variable de tipo String en el espacio de nombres DtsClient. En el ejemplo de código se usa Country como el nombre de la variable. (Puede que necesite haga clic en el **Elegir columnas de variables** botón de barra de herramientas en el **Variables** ventana para mostrar la **Namespace** columna.)  
  
3.  Agregue un administrador de conexiones OLE DB que se conecta a la base de datos de ejemplo [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)].  
  
4.  Agregue una tarea Flujo de datos al paquete y cambie a la superficie de diseño Flujo de datos.  
  
5.  Agregue un origen OLE DB al flujo de datos y configúrelo para utilizar el administrador de conexiones OLE DB creado anteriormente y el comando SQL siguiente:  
  
    ```  
    SELECT * FROM Sales.vIndividualCustomer WHERE CountryRegionName = ?  
    ```  
  
6.  Haga clic en **parámetros** y, en la **establecer parámetros de consulta** diálogo cuadro, el único parámetro de entrada en la consulta, Parameter0, se asigna a la variable dtsclient:: Country.  
  
7.  Agregue una transformación Agregado al flujo de datos y conecte la salida del origen OLE DB a la transformación. Abra el Editor de transformación Agregado y configúrelo para realizar una operación "COUNT ALL" en todas las columnas de entrada (*) y generar el valor de agregado con el alias CustomerCount.  
  
8.  Agregue un destino DataReader al flujo de datos y conecte la salida de transformación Agregado al destino DataReader. En el código de ejemplo se utiliza "DataReaderDest" como el nombre del DataReader. Seleccione una columna de entrada disponible única, CustomerCount, para el destino.  
  
9. Guarde el paquete. La aplicación de prueba creada a continuación ejecutará el paquete y recuperará la salida directamente de la memoria.  
  
#### <a name="to-create-the-test-application"></a>Para crear la aplicación de prueba  
  
1.  Cree una nueva aplicación Windows Forms.  
  
2.  Agregue una referencia a la **Microsoft.SqlServer.Dts.DtsClient** examinando el ensamblado del mismo nombre en el espacio de nombres **%ProgramFiles%\Microsoft SQL Server\100\DTS\Binn**.  
  
3.  Copie y pegue el código muestra siguiente en el módulo de código del formulario.  
  
4.  Modificar el valor de la **dtexecArgs** variable según sea necesario para que contenga los parámetros de línea de comandos requeridos por **dtexec.exe** para ejecutar el paquete. En el código muestra se carga el paquete desde el sistema de archivos.  
  
5.  Modificar el valor de la **dataReaderName** variable según sea necesario para que contenga el nombre del destino DataReader del paquete.  
  
6.  Coloque un botón y un cuadro de texto en el formulario. El código de ejemplo usa **btnRun** como el nombre del botón y **txtResults** como el nombre del cuadro de texto.  
  
7.  Ejecute la aplicación y haga clic en el botón. Después de una breve pausa mientras el paquete se ejecuta, debería aparecer en el cuadro de texto del formulario el valor agregado calculado por el paquete (el recuento de clientes de Canadá).  
  
### <a name="sample-code"></a>Código muestra  
  
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
  
## <a name="see-also"></a>Vea también  
 [Comprender las diferencias entre la ejecución Local y remota](../../integration-services/run-manage-packages-programmatically/understanding-the-differences-between-local-and-remote-execution.md)   
 [Cargar y ejecutar un paquete Local mediante programación](../../integration-services/run-manage-packages-programmatically/loading-and-running-a-local-package-programmatically.md)   
 [Cargar y ejecutar un paquete remoto mediante programación](../../integration-services/run-manage-packages-programmatically/loading-and-running-a-remote-package-programmatically.md)  
  
  

