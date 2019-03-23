---
title: Trabajar con archivos de Excel con la tarea Script | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- Script task [Integration Services], Excel files
- Script task [Integration Services], examples
- Excel [Integration Services]
ms.assetid: b8fa110a-2c9c-4f5a-8fe1-305555640e44
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 10fcf850a770296a81c99bc9b8168857b443df41
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/22/2019
ms.locfileid: "58376094"
---
# <a name="working-with-excel-files-with-the-script-task"></a>Trabajar con archivos de Excel con la tarea Script
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] proporciona el administrador de conexiones de Excel, el origen de Excel y el destino de Excel para trabajar con datos almacenados en hojas de cálculo en el formato de archivo de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel. Las técnicas descritas en este tema usan la tarea Script para obtener información acerca de las bases de datos de Excel disponibles (archivos de libro) y tablas (hojas de cálculo y rangos con nombre). Estos ejemplos se pueden modificar con facilidad para trabajar con cualquiera de los demás orígenes de datos basados en archivos que admite el proveedor OLE DB para [!INCLUDE[msCoName](../../includes/msconame-md.md)] Jet.  
  
 [Configurar un paquete para probar los ejemplos](#configuring)  
  
 [Ejemplo 1: Comprobar si existe un archivo de Excel](#example1)  
  
 [Ejemplo 2: Comprobar si existe una tabla de Excel](#example2)  
  
 [Ejemplo 3: Obtener una lista de archivos de Excel en una carpeta](#example3)  
  
 [Ejemplo 4: Obtener una lista de tablas en un archivo de Excel](#example4)  
  
 [Mostrar los resultados de los ejemplos](#testing)  
  
> [!NOTE]  
>  Si desea crear una tarea que pueda reutilizar más fácilmente en varios paquetes, considere la posibilidad de utilizar el código de este ejemplo de tarea Script como punto inicial de una tarea personalizada. Para más información, vea [Desarrollar una tarea personalizada](../extending-packages-custom-objects/task/developing-a-custom-task.md).  
  
##  <a name="configuring"></a>Configurar un paquete para probar los ejemplos  
 Puede configurar un paquete único para probar todos los ejemplos de este tema. En los ejemplos se usan muchas de las mismas variables de paquete y las mismas clases de [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)].  
  
#### <a name="to-configure-a-package-for-use-with-the-examples-in-this-topic"></a>Para configurar un paquete y utilizarlo con los ejemplos en este tema  
  
1.  Cree un nuevo proyecto de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] y abra el paquete predeterminado para editar.  
  
2.  **Variables**. Abra la ventana **Variables** y defina las variables siguientes:  
  
    -   `ExcelFile`, de tipo `String`. Escriba la ruta de acceso completa y nombre de archivo a un libro de Excel existente.  
  
    -   `ExcelTable`, de tipo `String`. Escriba el nombre de una hoja de cálculo existente o rango con nombre en el libro denominado en el valor de la variable `ExcelFile`. Este valor distingue mayúsculas de minúsculas.  
  
    -   `ExcelFileExists`, de tipo `Boolean`.  
  
    -   `ExcelTableExists`, de tipo `Boolean`.  
  
    -   `ExcelFolder`, de tipo `String`. Escriba la ruta de acceso completa de una carpeta que contiene por lo menos un libro de Excel.  
  
    -   `ExcelFiles`, de tipo `Object`.  
  
    -   `ExcelTables`, de tipo `Object`.  
  
3.  **Instrucciones Imports**. La mayoría de los ejemplos de código le exigen que importe uno o ambos de los espacios de nombres de [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] siguientes en la parte superior de su archivo de script:  
  
    -   `System.IO`, para operaciones del sistema de archivos.  
  
    -   `System.Data.OleDb`, para abrir los archivos de Excel como orígenes de datos.  
  
4.  **Referencias**. Los ejemplos de código que leen información de esquema de los archivos de Excel requieren una referencia adicional en el proyecto de script al espacio de nombres `System.Xml`.  
  
5.  Establezca el lenguaje de scripting predeterminado para el componente de script mediante la opción **Lenguaje de scripting** de la página **General** del cuadro de diálogo **Opciones**. Para obtener más información, vea[página General](../general-page-of-integration-services-designers-options.md).  
  
##  <a name="example1"></a> Ejemplo 1: Descripción: Comprobar si existe un archivo de Excel  
 En este ejemplo se determina si existe el archivo de libro de Excel especificado en la variable `ExcelFile` y, a continuación, se establece el valor booleano de la variable `ExcelFileExists` en el resultado. Puede usar este valor booleano para la bifurcación en el flujo de trabajo del paquete.  
  
#### <a name="to-configure-this-script-task-example"></a>Para configurar este ejemplo de tarea Script  
  
1.  Agregue una nueva tarea Script al paquete y cambie su nombre a `ExcelFileExists`.  
  
2.  En el **Editor de la tarea Script**, en la pestaña **Script**, haga clic en **ReadOnlyVariables** y escriba el valor de propiedad mediante uno de los métodos siguientes:  
  
    -   Tipo `ExcelFile`.  
  
         -o bien-  
  
    -   Haga clic en el botón de puntos suspensivos (**...** ) situado junto al campo de propiedad y, en el **seleccionar variables** cuadro de diálogo, seleccione el `ExcelFile` variable.  
  
3.  Haga clic en **ReadWriteVariables** y escriba el valor de propiedad mediante uno de los métodos siguientes:  
  
    -   Tipo `ExcelFileExists`.  
  
         -o bien-  
  
    -   Haga clic en el botón de puntos suspensivos (**...** ) situado junto al campo de propiedad y, en el **seleccionar variables** cuadro de diálogo, seleccione el `ExcelFileExists` variable.  
  
4.  Haga clic en **Modificar script** para abrir el editor de script.  
  
5.  Agregue una instrucción `Imports` para el espacio de nombres `System.IO` en la parte superior del archivo de script.  
  
6.  Agregue el código siguiente:  
  
### <a name="example-1-code"></a>Código de ejemplo 1  
  
```vb  
Public Class ScriptMain  
  Public Sub Main()  
    Dim fileToTest As String  
  
    fileToTest = Dts.Variables("ExcelFile").Value.ToString  
    If File.Exists(fileToTest) Then  
      Dts.Variables("ExcelFileExists").Value = True  
    Else  
      Dts.Variables("ExcelFileExists").Value = False  
    End If  
  
    Dts.TaskResult = ScriptResults.Success  
  End Sub  
End Class  
```  
  
```csharp  
public class ScriptMain  
{  
  public void Main()  
  {  
    string fileToTest;  
  
    fileToTest = Dts.Variables["ExcelFile"].Value.ToString();  
    if (File.Exists(fileToTest))  
    {  
      Dts.Variables["ExcelFileExists"].Value = true;  
    }  
    else  
    {  
      Dts.Variables["ExcelFileExists"].Value = false;  
    }  
  
    Dts.TaskResult = (int)ScriptResults.Success;  
  }  
}  
```  
  
##  <a name="example2"></a> Ejemplo 2: Descripción: Comprobar si existe una tabla de Excel  
 En este ejemplo se determina si existe la hoja de cálculo de Excel o el rango con nombre especificado en la variable `ExcelTable` en el archivo de libro de Excel especificado en la variable `ExcelFile` y, a continuación, se establece el valor booleano de la variable `ExcelTableExists` en el resultado. Puede usar este valor booleano para la bifurcación en el flujo de trabajo del paquete.  
  
#### <a name="to-configure-this-script-task-example"></a>Para configurar este ejemplo de tarea Script  
  
1.  Agregue una nueva tarea Script al paquete y cambie su nombre a `ExcelTableExists`.  
  
2.  En el **Editor de la tarea Script**, en la pestaña **Script**, haga clic en **ReadOnlyVariables** y escriba el valor de propiedad mediante uno de los métodos siguientes:  
  
    -   Tipo `ExcelTable` y `ExcelFile` separados por comas`.`  
  
         -o bien-  
  
    -   Haga clic en el botón de puntos suspensivos (**...** ) situado junto al campo de propiedad y, en el **seleccionar variables** cuadro de diálogo, seleccione el `ExcelTable` y `ExcelFile` variables.  
  
3.  Haga clic en **ReadWriteVariables** y escriba el valor de propiedad mediante uno de los métodos siguientes:  
  
    -   Tipo `ExcelTableExists`.  
  
         -o bien-  
  
    -   Haga clic en el botón de puntos suspensivos (**...** ) situado junto al campo de propiedad y, en el **seleccionar variables** cuadro de diálogo, seleccione el `ExcelTableExists` variable.  
  
4.  Haga clic en **Modificar script** para abrir el editor de script.  
  
5.  Agregue una referencia al ensamblado `System.Xml` en el proyecto de script.  
  
6.  Agregue instrucciones `Imports` para los espacios de nombres `System.IO` y `System.Data.OleDb` en la parte superior del archivo de script.  
  
7.  Agregue el código siguiente:  
  
### <a name="example-2-code"></a>Código de ejemplo 2  
  
```vb  
Public Class ScriptMain  
  Public Sub Main()  
    Dim fileToTest As String  
    Dim tableToTest As String  
    Dim connectionString As String  
    Dim excelConnection As OleDbConnection  
    Dim excelTables As DataTable  
    Dim excelTable As DataRow  
    Dim currentTable As String  
  
    fileToTest = Dts.Variables("ExcelFile").Value.ToString  
    tableToTest = Dts.Variables("ExcelTable").Value.ToString  
  
    Dts.Variables("ExcelTableExists").Value = False  
    If File.Exists(fileToTest) Then  
      connectionString = "Provider=Microsoft.Jet.OLEDB.4.0;" & _  
        "Data Source=" & fileToTest & _  
        ";Extended Properties=Excel 8.0"  
      excelConnection = New OleDbConnection(connectionString)  
      excelConnection.Open()  
      excelTables = excelConnection.GetSchema("Tables")  
      For Each excelTable In excelTables.Rows  
        currentTable = excelTable.Item("TABLE_NAME").ToString  
        If currentTable = tableToTest Then  
          Dts.Variables("ExcelTableExists").Value = True  
        End If  
      Next  
    End If  
  
    Dts.TaskResult = ScriptResults.Success  
  End Sub  
End Class  
```  
  
```csharp  
public class ScriptMain  
{  
    public void Main()  
        {  
            string fileToTest;  
            string tableToTest;  
            string connectionString;  
            OleDbConnection excelConnection;  
            DataTable excelTables;  
            string currentTable;  
  
            fileToTest = Dts.Variables["ExcelFile"].Value.ToString();  
            tableToTest = Dts.Variables["ExcelTable"].Value.ToString();  
  
            Dts.Variables["ExcelTableExists"].Value = false;  
            if (File.Exists(fileToTest))  
            {  
                connectionString = "Provider=Microsoft.Jet.OLEDB.4.0;" +  
                "Data Source=" + fileToTest + ";Extended Properties=Excel 8.0";  
                excelConnection = new OleDbConnection(connectionString);  
                excelConnection.Open();  
                excelTables = excelConnection.GetSchema("Tables");  
                foreach (DataRow excelTable in excelTables.Rows)  
                {  
                    currentTable = excelTable["TABLE_NAME"].ToString();  
                    if (currentTable == tableToTest)  
                    {  
                        Dts.Variables["ExcelTableExists"].Value = true;  
                    }  
                }  
            }  
  
            Dts.TaskResult = (int)ScriptResults.Success;  
  
        }  
}  
```  
  
##  <a name="example3"></a> Descripción de ejemplo 3: Obtener una lista de archivos de Excel en una carpeta  
 En este ejemplo se llena una matriz con la lista de archivos de Excel ubicados en la carpeta especificada del valor de la variable `ExcelFolder` y, a continuación, se copia la matriz en la variable `ExcelFiles`. Puede usar el enumerador de variable para Foreach para iterar sobre los archivos en la matriz.  
  
#### <a name="to-configure-this-script-task-example"></a>Para configurar este ejemplo de tarea Script  
  
1.  Agregue una nueva tarea Script al paquete y cambie su nombre a **GetExcelFiles**.  
  
2.  Abra el **Editor de la tarea Script**, en la pestaña **Script**, haga clic en **ReadOnlyVariables** y escriba el valor de propiedad mediante uno de los métodos siguientes:  
  
    -   Escriba `ExcelFolder`  
  
         -o bien-  
  
    -   Haga clic en el botón de puntos suspensivos (**…**) junto al campo de propiedades y, en el cuadro de diálogo **Seleccionar variables**, seleccione la variable ExcelFolder.  
  
3.  Haga clic en **ReadWriteVariables** y escriba el valor de propiedad mediante uno de los métodos siguientes:  
  
    -   Tipo `ExcelFiles`.  
  
         -o bien-  
  
    -   Haga clic en el botón de puntos suspensivos (**…**) junto al campo de propiedades y, en el cuadro de diálogo **Seleccionar variables**, seleccione la variable ExcelFiles.  
  
4.  Haga clic en **Modificar script** para abrir el editor de script.  
  
5.  Agregue una instrucción `Imports` para el espacio de nombres `System.IO` en la parte superior del archivo de script.  
  
6.  Agregue el código siguiente:  
  
### <a name="example-3-code"></a>Código de ejemplo 3  
  
```vb  
Public Class ScriptMain  
  Public Sub Main()  
    Const FILE_PATTERN As String = "*.xls"  
  
    Dim excelFolder As String  
    Dim excelFiles As String()  
  
    excelFolder = Dts.Variables("ExcelFolder").Value.ToString  
    excelFiles = Directory.GetFiles(excelFolder, FILE_PATTERN)  
  
    Dts.Variables("ExcelFiles").Value = excelFiles  
  
    Dts.TaskResult = ScriptResults.Success  
  End Sub  
End Class  
```  
  
```csharp  
public class ScriptMain  
{  
  public void Main()  
  {  
    const string FILE_PATTERN = "*.xls";  
  
    string excelFolder;  
    string[] excelFiles;  
  
    excelFolder = Dts.Variables["ExcelFolder"].Value.ToString();  
    excelFiles = Directory.GetFiles(excelFolder, FILE_PATTERN);  
  
    Dts.Variables["ExcelFiles"].Value = excelFiles;  
  
    Dts.TaskResult = (int)ScriptResults.Success;  
  }  
}  
```  
  
### <a name="alternate-solution"></a>Solución alternativa  
 En lugar de usar una tarea Script para recopilar una lista de archivos de Excel en una matriz, puede usar también el enumerador de archivos ForEach para iterar sobre todos los archivos de Excel de una carpeta. Para obtener más información, consulte [Loop through Excel Files and Tables by Using a Foreach Loop Container](../control-flow/foreach-loop-container.md) (Crear bucles entre archivos y tablas de Excel usando un contenedor de bucles Para cada uno).  
  
##  <a name="example4"></a> Descripción de ejemplo 4: Obtener una lista de tablas en un archivo de Excel  
 En este ejemplo se llena una matriz con la lista de hojas de cálculo y rangos con nombre ubicados en el archivo de libro de Excel especificado por el valor de la variable `ExcelFile` y, a continuación, se copia la matriz en la variable `ExcelTables`. Puede usar el enumerador de variable para Foreach para iterar sobre las tablas en la matriz.  
  
> [!NOTE]  
>  La lista de tablas de un libro de Excel incluye tanto hojas (que tienen el sufijo $) como rangos con nombre. Si tiene que filtrar la lista para obtener solo las hojas o solo los rangos con nombre, agregue código adicional para este fin.  
  
#### <a name="to-configure-this-script-task-example"></a>Para configurar este ejemplo de tarea Script  
  
1.  Agregue una nueva tarea Script al paquete y cambie su nombre a **GetExcelTables**.  
  
2.  Abra el **Editor de la tarea Script**, en la pestaña **Script**, haga clic en **ReadOnlyVariables** y escriba el valor de propiedad mediante uno de los métodos siguientes:  
  
    -   Tipo `ExcelFile`.  
  
         -o bien-  
  
    -   Haga clic en el botón de puntos suspensivos (**…**) junto al campo de propiedades y, en el cuadro de diálogo **Seleccionar variables**, seleccione la variable ExcelFile.  
  
3.  Haga clic en **ReadWriteVariables** y escriba el valor de propiedad mediante uno de los métodos siguientes:  
  
    -   Tipo `ExcelTables`.  
  
         -o bien-  
  
    -   Haga clic en el botón de puntos suspensivos (**…**) junto al campo de propiedades y, en el cuadro de diálogo **Seleccionar variables**, seleccione la variable ExcelTablesvariable.  
  
4.  Haga clic en **Modificar script** para abrir el editor de script.  
  
5.  Agregue una referencia al espacio de nombres `System.Xml` en el proyecto de script.  
  
6.  Agregue una instrucción `Imports` para el espacio de nombres `System.Data.OleDb` en la parte superior del archivo de script.  
  
7.  Agregue el código siguiente:  
  
### <a name="example-4-code"></a>Código de ejemplo 4  
  
```vb  
Public Class ScriptMain  
  Public Sub Main()  
    Dim excelFile As String  
    Dim connectionString As String  
    Dim excelConnection As OleDbConnection  
    Dim tablesInFile As DataTable  
    Dim tableCount As Integer = 0  
    Dim tableInFile As DataRow  
    Dim currentTable As String  
    Dim tableIndex As Integer = 0  
  
    Dim excelTables As String()  
  
    excelFile = Dts.Variables("ExcelFile").Value.ToString  
    connectionString = "Provider=Microsoft.Jet.OLEDB.4.0;" & _  
        "Data Source=" & excelFile & _  
        ";Extended Properties=Excel 8.0"  
    excelConnection = New OleDbConnection(connectionString)  
    excelConnection.Open()  
    tablesInFile = excelConnection.GetSchema("Tables")  
    tableCount = tablesInFile.Rows.Count  
    ReDim excelTables(tableCount - 1)  
    For Each tableInFile In tablesInFile.Rows  
      currentTable = tableInFile.Item("TABLE_NAME").ToString  
      excelTables(tableIndex) = currentTable  
      tableIndex += 1  
    Next  
  
    Dts.Variables("ExcelTables").Value = excelTables  
  
    Dts.TaskResult = ScriptResults.Success  
  End Sub  
End Class  
```  
  
```csharp  
public class ScriptMain  
{  
  public void Main()  
        {  
            string excelFile;  
            string connectionString;  
            OleDbConnection excelConnection;  
            DataTable tablesInFile;  
            int tableCount = 0;  
            string currentTable;  
            int tableIndex = 0;  
  
            string[] excelTables = new string[5];  
  
            excelFile = Dts.Variables["ExcelFile"].Value.ToString();  
            connectionString = "Provider=Microsoft.Jet.OLEDB.4.0;" +  
                "Data Source=" + excelFile + ";Extended Properties=Excel 8.0";  
            excelConnection = new OleDbConnection(connectionString);  
            excelConnection.Open();  
            tablesInFile = excelConnection.GetSchema("Tables");  
            tableCount = tablesInFile.Rows.Count;  
  
            foreach (DataRow tableInFile in tablesInFile.Rows)  
            {  
                currentTable = tableInFile["TABLE_NAME"].ToString();  
                excelTables[tableIndex] = currentTable;  
                tableIndex += 1;  
            }  
  
            Dts.Variables["ExcelTables"].Value = excelTables;  
  
            Dts.TaskResult = (int)ScriptResults.Success;  
        }  
}  
```  
  
### <a name="alternate-solution"></a>Solución alternativa  
 En lugar de usar una tarea Script para recopilar una lista de tablas Excel en una matriz, puede usar también el enumerador de conjunto de filas de esquema para Foreach de ADO.NET para iterar sobre todas las tablas (es decir, hojas de cálculo y rangos con nombre) en un archivo de libro de Excel. Para obtener más información, consulte [Loop through Excel Files and Tables by Using a Foreach Loop Container](../control-flow/foreach-loop-container.md) (Crear bucles entre archivos y tablas de Excel usando un contenedor de bucles Para cada uno).  
  
##  <a name="testing"></a> Mostrar los resultados de los ejemplos  
 Si ha configurado cada uno de los ejemplos de este tema en el mismo paquete, puede conectar todas las tareas Script a una tarea Script adicional que muestra la salida de todos los ejemplos.  
  
#### <a name="to-configure-a-script-task-to-display-the-output-of-the-examples-in-this-topic"></a>Para configurar una tarea Script para mostrar la salida de los ejemplos de este tema  
  
1.  Agregue una nueva tarea Script al paquete y cambie su nombre a **DisplayResults**.  
  
2.  Conecte entre sí cada una de las tareas Script de los cuatro ejemplos, de manera que cada tarea se ejecute después de que la tarea anterior se complete correctamente, y conecte la tarea del ejemplo cuatro a la tarea **DisplayResults**.  
  
3.  Abra la tarea **DisplayResults** del **Editor de la tarea Script**.  
  
4.  En la pestaña **Script**, haga clic en **ReadOnlyVariables** y use uno de los métodos siguientes para agregar las siete variables enumeradas en [Configurar un paquete para probar los ejemplos](#configuring):  
  
    -   Escriba el nombre de cada variable separado por comas.  
  
         -o bien-  
  
    -   Haga clic en el botón de puntos suspensivos (**…**) junto al campo de propiedades y, en el cuadro de diálogo **Seleccionar variables**, seleccione las variables.  
  
5.  Haga clic en **Modificar script** para abrir el editor de script.  
  
6.  Agregue instrucciones `Imports` para los espacios de nombres `Microsoft.VisualBasic` y `System.Windows.Forms` en la parte superior del archivo de script.  
  
7.  Agregue el código siguiente:  
  
8.  Ejecute el paquete y examine los resultados que aparecen en un cuadro de mensaje.  
  
### <a name="code-to-display-the-results"></a>Código para mostrar los resultados  
  
```vb  
Public Class ScriptMain  
  Public Sub Main()  
    Const EOL As String = ControlChars.CrLf  
  
    Dim results As String  
    Dim filesInFolder As String()  
    Dim fileInFolder As String  
    Dim tablesInFile As String()  
    Dim tableInFile As String  
  
    results = _  
      "Final values of variables:" & EOL & _  
      "ExcelFile: " & Dts.Variables("ExcelFile").Value.ToString & EOL & _  
      "ExcelFileExists: " & Dts.Variables("ExcelFileExists").Value.ToString & EOL & _  
      "ExcelTable: " & Dts.Variables("ExcelTable").Value.ToString & EOL & _  
      "ExcelTableExists: " & Dts.Variables("ExcelTableExists").Value.ToString & EOL & _  
      "ExcelFolder: " & Dts.Variables("ExcelFolder").Value.ToString & EOL & _  
      EOL  
  
    results &= "Excel files in folder: " & EOL  
    filesInFolder = DirectCast(Dts.Variables("ExcelFiles").Value, String())  
    For Each fileInFolder In filesInFolder  
      results &= " " & fileInFolder & EOL  
    Next  
    results &= EOL  
  
    results &= "Excel tables in file: " & EOL  
    tablesInFile = DirectCast(Dts.Variables("ExcelTables").Value, String())  
    For Each tableInFile In tablesInFile  
      results &= " " & tableInFile & EOL  
    Next  
  
    MessageBox.Show(results, "Results", MessageBoxButtons.OK, MessageBoxIcon.Information)  
  
    Dts.TaskResult = ScriptResults.Success  
  End Sub  
End Class  
```  
  
```csharp  
public class ScriptMain  
{  
  public void Main()  
        {  
            const string EOL = "\r";  
  
            string results;  
            string[] filesInFolder;  
            //string fileInFolder;  
            string[] tablesInFile;  
            //string tableInFile;  
  
            results = "Final values of variables:" + EOL + "ExcelFile: " + Dts.Variables["ExcelFile"].Value.ToString() + EOL + "ExcelFileExists: " + Dts.Variables["ExcelFileExists"].Value.ToString() + EOL + "ExcelTable: " + Dts.Variables["ExcelTable"].Value.ToString() + EOL + "ExcelTableExists: " + Dts.Variables["ExcelTableExists"].Value.ToString() + EOL + "ExcelFolder: " + Dts.Variables["ExcelFolder"].Value.ToString() + EOL + EOL;  
  
            results += "Excel files in folder: " + EOL;  
            filesInFolder = (string[])(Dts.Variables["ExcelFiles"].Value);  
            foreach (string fileInFolder in filesInFolder)  
            {  
                results += " " + fileInFolder + EOL;  
            }  
            results += EOL;  
  
            results += "Excel tables in file: " + EOL;  
            tablesInFile = (string[])(Dts.Variables["ExcelTables"].Value);  
            foreach (string tableInFile in tablesInFile)  
            {  
                results += " " + tableInFile + EOL;  
            }  
  
            MessageBox.Show(results, "Results", MessageBoxButtons.OK, MessageBoxIcon.Information);  
  
            Dts.TaskResult = (int)ScriptResults.Success;  
        }  
}  
```  
  
![Icono de Integration Services (pequeño)](../media/dts-16.gif "icono de Integration Services (pequeño)")**mantenerse actualizado con Integration Services**<br /> Para obtener las descargas, artículos, ejemplos y vídeos más recientes de Microsoft, así como soluciones seleccionadas de la comunidad, visite la página de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] en MSDN:<br /><br /> [Visite la página de Integration Services en MSDN](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Para recibir notificaciones automáticas de estas actualizaciones, suscríbase a las fuentes RSS disponibles en la página.  
  
## <a name="see-also"></a>Vea también  
 [Administrador de conexiones de Excel](../connection-manager/excel-connection-manager.md)   
 [Crear bucles entre archivos y tablas de Excel mediante un contenedor de bucles ForEach](../control-flow/foreach-loop-container.md)  
  
  
