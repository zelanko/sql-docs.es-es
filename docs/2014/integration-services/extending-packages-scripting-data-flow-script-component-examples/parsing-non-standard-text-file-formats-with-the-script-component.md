---
title: Analizar formatos de archivo de texto no estándar con el componente de script | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- docset-sql-devref
- integration-services
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- text file reading [Integration Services]
- Script component [Integration Services], non-standard text file formats
- transformations [Integration Services], components
- Script component [Integration Services], examples
ms.assetid: 1fda034d-09e4-4647-9a9f-e8d508c2cc8f
caps.latest.revision: 35
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 6c34669ffc14ee623b17549f588385886488ed02
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37287601"
---
# <a name="parsing-non-standard-text-file-formats-with-the-script-component"></a>Analizar formatos de archivo de texto no estándar con el componente de script
  Cuando los datos de origen están organizados en un formato no estándar, puede resultar más cómodo consolidar toda la lógica de análisis en un único script que encadenar varias transformaciones de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] para lograr el mismo resultado.  
  
 [Ejemplo 1: Analizar registros delimitados por fila](#example1)  
  
 [Ejemplo 2: Dividir registros primarios y secundarios](#example2)  
  
> [!NOTE]  
>  Si desea crear un componente que pueda reutilizar más fácilmente en varias tareas de flujo de datos y varios paquetes, puede utilizar el código de este ejemplo de componente de script como punto de inicio para el componente de flujo de datos personalizado. Para obtener más información, vea [Desarrollar un componente de flujo de datos personalizado](../extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md).  
  
##  <a name="example1"></a> Ejemplo 1: Analizar registros delimitados por fila  
 En este ejemplo se muestra cómo tomar un archivo de texto en el que cada columna de datos aparece en una línea independiente y analizarlo en una tabla de destino utilizando el componente de script.  
  
 Para obtener más información acerca de cómo configurar el componente de Script para su uso como una transformación del flujo de datos, vea [crear una transformación sincrónica con el componente de Script](../extending-packages-scripting-data-flow-script-component-types/creating-a-synchronous-transformation-with-the-script-component.md)y [creando una asincrónica Transformación con el componente de Script](../extending-packages-scripting-data-flow-script-component-types/creating-an-asynchronous-transformation-with-the-script-component.md).  
  
#### <a name="to-configure-this-script-component-example"></a>Para configurar este ejemplo de componente de script  
  
1.  Cree y guarde un archivo de texto denominado **rowdelimiteddata.txt** que contenga los siguientes datos de origen:  
  
    ```  
    FirstName: Nancy  
    LastName: Davolio  
    Title: Sales Representative  
    City: Seattle  
    StateProvince: WA  
  
    FirstName: Andrew  
    LastName: Fuller  
    Title: Vice President, Sales  
    City: Tacoma  
    StateProvince: WA  
  
    FirstName: Steven  
    LastName: Buchanan  
    Title: Sales Manager  
    City: London  
    StateProvince:  
  
    ```  
  
2.  Abra [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] y conéctese a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
3.  Seleccione una base de datos de destino y abra una nueva ventana de consulta. En la ventana de consulta, ejecute el siguiente script para crear la tabla de destino:  
  
    ```  
    create table RowDelimitedData  
    (  
    FirstName varchar(32),  
    LastName varchar(32),  
    Title varchar(32),  
    City varchar(32),  
    StateProvince varchar(32)  
    )  
  
    ```  
  
4.  Abra [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] y cree un nuevo paquete de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] denominado ParseRowDelim.dtsx.  
  
5.  Agregue un administrador de conexiones de archivos planos al paquete, denomínelo RowDelimitedData y configúrelo para conectarse al archivo rowdelimiteddata.txt que creó en un paso anterior.  
  
6.  Agregue un administrador de conexiones OLE DB al paquete y configúrelo para conectarse a la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y a la base de datos donde creó la tabla de destino.  
  
7.  Agregue una tarea de flujo de datos al paquete y haga clic en la pestaña **Flujo de datos** del Diseñador SSIS.  
  
8.  Agregue un origen de archivo plano al flujo de datos y configúrelo para utilizar el administrador de conexiones RowDelimitedData. En la página **Columnas** del **Editor de origen de archivos planos**, seleccione la única columna externa disponible.  
  
9. Agregue un componente de script al flujo de datos y configúrelo como una transformación. Conecte la salida del origen de archivo plano al componente de script.  
  
10. Haga doble clic en el componente de script para mostrar el **Editor de transformación Script**.  
  
11. En la página **Columnas de entrada** del **Editor de transformación Script**, seleccione la única columna de entrada disponible.  
  
12. En el **entradas y salidas** página de la **Editor de transformación Script**, seleccione salida 0 y establezca su `SynchronousInputID` en None. Cree 5 columnas de salida, todas del tipo cadena [DT_STR] con una longitud de 32:  
  
    -   FirstName  
  
    -   LastName  
  
    -   Title  
  
    -   City  
  
    -   StateProvince  
  
13. En el **Script** página de la **Editor de transformación Script**, haga clic en **editar Script** y escriba el código se muestra en el `ScriptMain` clase del ejemplo. Cierre el entorno de desarrollo de script y el **Editor de transformación Script**.  
  
14. Agregue un destino de SQL Server al flujo de datos. Configúrelo para utilizar el administrador de conexiones OLE DB y la tabla RowDelimitedData. Conecte la salida del componente de script a este destino.  
  
15. Ejecute el paquete. Después de que el paquete haya finalizado, examine los registros en la tabla de destino de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
```vb  
Public Overrides Sub Input0_ProcessInputRow(ByVal Row As Input0Buffer)  
  
    Dim columnName As String  
    Dim columnValue As String  
  
    ' Check for an empty row.  
    If Row.Column0.Trim.Length > 0 Then  
        columnName = Row.Column0.Substring(0, Row.Column0.IndexOf(":"))  
        ' Check for an empty value after the colon.  
        If Row.Column0.Substring(Row.Column0.IndexOf(":")).TrimEnd.Length > 1 Then  
            ' Extract the column value from after the colon and space.  
            columnValue = Row.Column0.Substring(Row.Column0.IndexOf(":") + 2)  
            Select Case columnName  
                Case "FirstName"  
                    ' The FirstName value indicates a new record.  
                    Me.Output0Buffer.AddRow()  
                    Me.Output0Buffer.FirstName = columnValue  
                Case "LastName"  
                    Me.Output0Buffer.LastName = columnValue  
                Case "Title"  
                    Me.Output0Buffer.Title = columnValue  
                Case "City"  
                    Me.Output0Buffer.City = columnValue  
                Case "StateProvince"  
                    Me.Output0Buffer.StateProvince = columnValue  
            End Select  
        End If  
    End If  
  
End Sub  
```  
  
```csharp  
public override void Input0_ProcessInputRow(Input0Buffer Row)  
    {  
  
        string columnName;  
        string columnValue;  
  
        // Check for an empty row.  
        if (Row.Column0.Trim().Length > 0)  
        {  
            columnName = Row.Column0.Substring(0, Row.Column0.IndexOf(":"));  
            // Check for an empty value after the colon.  
            if (Row.Column0.Substring(Row.Column0.IndexOf(":")).TrimEnd().Length > 1)  
            // Extract the column value from after the colon and space.  
            {  
                columnValue = Row.Column0.Substring(Row.Column0.IndexOf(":") + 2);  
                switch (columnName)  
                {  
                    case "FirstName":  
                        // The FirstName value indicates a new record.  
                        this.Output0Buffer.AddRow();  
                        this.Output0Buffer.FirstName = columnValue;  
                        break;  
                    case "LastName":  
                        this.Output0Buffer.LastName = columnValue;  
                        break;  
                    case "Title":  
                        this.Output0Buffer.Title = columnValue;  
                        break;  
                    case "City":  
                        this.Output0Buffer.City = columnValue;  
                        break;  
                    case "StateProvince":  
                        this.Output0Buffer.StateProvince = columnValue;  
                        break;  
                }  
            }  
        }  
  
    }  
```  
  
##  <a name="example2"></a> Ejemplo 2: Dividir registros primarios y secundarios  
 Este ejemplo muestra cómo tomar un archivo de texto, en el que una fila de separación precede a una fila de registro primario a la que siguen un número indefinido de filas de registro secundario, y cómo analizarlo en tablas de destino primarias y secundarias correctamente normalizadas mediante el componente de script. Este sencillo ejemplo se puede adaptar fácilmente a archivos de origen que utilizan más de una fila o columna para cada registro primario y secundario, siempre que exista una forma de identificar el principio y el final de cada registro.  
  
> [!CAUTION]  
>  El único fin de este ejemplo es usarlo para realizar una demostración. Si ejecuta más de una vez el ejemplo, se insertan valores de clave duplicados en la tabla de destino.  
  
 Para obtener más información acerca de cómo configurar el componente de Script para su uso como una transformación del flujo de datos, vea [crear una transformación sincrónica con el componente de Script](../extending-packages-scripting-data-flow-script-component-types/creating-a-synchronous-transformation-with-the-script-component.md)y [creando una asincrónica Transformación con el componente de Script](../extending-packages-scripting-data-flow-script-component-types/creating-an-asynchronous-transformation-with-the-script-component.md).  
  
#### <a name="to-configure-this-script-component-example"></a>Para configurar este ejemplo de componente de script  
  
1.  Cree y guarde un archivo de texto denominado **prentchilddata.txt** que contenga los siguientes datos de origen:  
  
    ```  
    **********  
    PARENT 1 DATA  
    child 1 data  
    child 2 data  
    child 3 data  
    child 4 data  
    **********  
    PARENT 2 DATA  
    child 5 data  
    child 6 data  
    child 7 data  
    child 8 data  
    **********  
  
    ```  
  
2.  Abra [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] y conéctese a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
3.  Seleccione una base de datos de destino y abra una nueva ventana de consulta. En la ventana de consulta, ejecute el siguiente script para crear las tablas de destino:  
  
    ```  
    CREATE TABLE [dbo].[Parents]([ParentID] [int] NOT NULL,  
    [ParentRecord] [varchar](32) NOT NULL,  
     CONSTRAINT [PK_Parents] PRIMARY KEY CLUSTERED   
    ([ParentID] ASC))  
    GO  
    CREATE TABLE [dbo].[Children]([ChildID] [int] NOT NULL,  
    [ParentID] [int] NOT NULL,  
    [ChildRecord] [varchar](32) NOT NULL,  
     CONSTRAINT [PK_Children] PRIMARY KEY CLUSTERED   
    ([ChildID] ASC))  
    GO  
    ALTER TABLE [dbo].[Children] ADD CONSTRAINT [FK_Children_Parents] FOREIGN KEY([ParentID])  
    REFERENCES [dbo].[Parents] ([ParentID])  
  
    ```  
  
4.  Abra [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] y cree un nuevo paquete de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] denominado SplitParentChild.dtsx.  
  
5.  Agregue un administrador de conexiones de archivos planos al paquete, denomínelo ParentChildData y configúrelo para conectarse al archivo parentchilddata.txt que creó en un paso anterior.  
  
6.  Agregue un administrador de conexiones OLE DB al paquete y configúrelo para conectarse a la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y a la base de datos donde creó las tablas de destino.  
  
7.  Agregue una tarea de flujo de datos al paquete y haga clic en la pestaña **Flujo de datos** del Diseñador SSIS.  
  
8.  Agregue un origen de archivo plano al flujo de datos y configúrelo para utilizar el administrador de conexiones ParentChildData. En la página **Columnas** del **Editor de origen de archivos planos**, seleccione la única columna externa disponible.  
  
9. Agregue un componente de script al flujo de datos y configúrelo como una transformación. Conecte la salida del origen de archivo plano al componente de script.  
  
10. Haga doble clic en el componente de script para mostrar el **Editor de transformación Script**.  
  
11. En la página **Columnas de entrada** del **Editor de transformación Script**, seleccione la única columna de entrada disponible.  
  
12. En el **entradas y salidas** página de la **Editor de transformación Script**, seleccione salida 0, cámbiele el nombre a ParentRecords y establezca su `SynchronousInputID` en None. Cree 2 columnas de salida:  
  
    -   ParentID (la clave principal), de tipo entero de cuatro bytes con signo [DT_I4]  
  
    -   ParentRecord, de tipo cadena [DT_STR] con una longitud de 32.  
  
13. Cree una segunda salida y denomínela ChildRecords. El valor `SynchronousInputID` de la nueva salida ya está establecido en Ninguno. Cree 3 columnas de salida:  
  
    -   ChildID (la clave principal), de tipo entero de cuatro bytes con signo [DT_I4]  
  
    -   ParentID (la clave externa), también de tipo entero de cuatro bytes con signo [DT_I4]  
  
    -   ChildRecord, de tipo cadena [DT_STR] con una longitud de 50.  
  
14. En la página **Script** del **Editor de transformación Script**, haga clic en **Editar script**. En la clase `ScriptMain`, escriba el código mostrado en el ejemplo. Cierre el entorno de desarrollo de script y el **Editor de transformación Script**.  
  
15. Agregue un destino de SQL Server al flujo de datos. Conecte la salida ParentRecords del componente de script a este destino. Configúrela para utilizar el administrador de conexiones OLE DB y la tabla Parents.  
  
16. Agregue otro destino de SQL Server al flujo de datos. Conecte la salida ChildRecords del componente de script a este destino. Configúrela para utilizar el administrador de conexiones OLE DB y la tabla Children.  
  
17. Ejecute el paquete. Después de que el paquete haya finalizado, examine los registros primarios y secundarios en las dos tablas de destino de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
```vb  
Public Overrides Sub Input0_ProcessInputRow(ByVal Row As Input0Buffer)  
  
    Static nextRowIsParent As Boolean = False  
    Static parentCounter As Integer = 0  
    Static childCounter As Integer = 0  
  
    ' If current row starts with separator characters,  
    '  then following row contains new parent record.  
    If Row.Column0.StartsWith("***") Then  
        nextRowIsParent = True  
    Else  
        If nextRowIsParent Then  
            ' Current row contains parent record.  
            parentCounter += 1  
            Me.ParentRecordsBuffer.AddRow()  
            Me.ParentRecordsBuffer.ParentID = parentCounter  
            Me.ParentRecordsBuffer.ParentRecord = Row.Column0  
            nextRowIsParent = False  
        Else  
            ' Current row contains child record.  
            childCounter += 1  
            Me.ChildRecordsBuffer.AddRow()  
            Me.ChildRecordsBuffer.ChildID = childCounter  
            Me.ChildRecordsBuffer.ParentID = parentCounter  
            Me.ChildRecordsBuffer.ChildRecord = Row.Column0  
        End If  
    End If  
  
End Sub  
```  
  
```csharp  
public override void Input0_ProcessInputRow(Input0Buffer Row)  
    {  
  
    int static_Input0_ProcessInputRow_childCounter = 0;  
    int static_Input0_ProcessInputRow_parentCounter = 0;  
    bool static_Input0_ProcessInputRow_nextRowIsParent = false;  
  
        // If current row starts with separator characters,   
        // then following row contains new parent record.   
        if (Row.Column0.StartsWith("***"))  
        {  
            static_Input0_ProcessInputRow_nextRowIsParent = true;  
        }  
        else  
        {  
            if (static_Input0_ProcessInputRow_nextRowIsParent)  
            {  
                // Current row contains parent record.   
                static_Input0_ProcessInputRow_parentCounter += 1;  
                this.ParentRecordsBuffer.AddRow();  
                this.ParentRecordsBuffer.ParentID = static_Input0_ProcessInputRow_parentCounter;  
                this.ParentRecordsBuffer.ParentRecord = Row.Column0;  
                static_Input0_ProcessInputRow_nextRowIsParent = false;  
            }  
            else  
            {  
                // Current row contains child record.   
                static_Input0_ProcessInputRow_childCounter += 1;  
                this.ChildRecordsBuffer.AddRow();  
                this.ChildRecordsBuffer.ChildID = static_Input0_ProcessInputRow_childCounter;  
                this.ChildRecordsBuffer.ParentID = static_Input0_ProcessInputRow_parentCounter;  
                this.ChildRecordsBuffer.ChildRecord = Row.Column0;  
            }  
        }  
  
    }  
```  
  
![Icono de Integration Services (pequeño)](../media/dts-16.gif "icono de Integration Services (pequeño)")**mantenerse actualizado con Integration Services  **<br /> Para obtener las descargas, artículos, ejemplos y vídeos más recientes de Microsoft, así como soluciones seleccionadas de la comunidad, visite la página de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] en MSDN:<br /><br /> [Visite la página de Integration Services en MSDN](http://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Para recibir notificaciones automáticas de estas actualizaciones, suscríbase a las fuentes RSS disponibles en la página.  
  
## <a name="see-also"></a>Vea también  
 [Crear una transformación sincrónica con el componente de script](../extending-packages-scripting-data-flow-script-component-types/creating-a-synchronous-transformation-with-the-script-component.md)  
 [Crear una transformación asincrónica con el componente de script](../extending-packages-scripting-data-flow-script-component-types/creating-an-asynchronous-transformation-with-the-script-component.md)  
  
  
