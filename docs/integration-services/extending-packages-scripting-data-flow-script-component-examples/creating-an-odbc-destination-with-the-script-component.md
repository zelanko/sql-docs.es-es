---
title: Crear un destino ODBC con el componente de Script | Documentos de Microsoft
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
helpviewer_keywords:
- Script component [Integration Services], destination components
- ODBC destination [Integration Services]
- destinations [Integration Services], components
- Script component [Integration Services], examples
ms.assetid: d198c866-78f4-4a50-ae15-333160645815
caps.latest.revision: 42
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 5eb539f0d18f473b10ed8d49bcee9c298292fb41
ms.contentlocale: es-es
ms.lasthandoff: 09/26/2017

---
# <a name="creating-an-odbc-destination-with-the-script-component"></a>Crear un destino ODBC con el componente de script
  En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], normalmente guardar datos en un destino ODBC mediante una [!INCLUDE[vstecado](../../includes/vstecado-md.md)] destino y el [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] proveedor de datos de ODBC. Sin embargo, también se puede crear un destino ODBC ad hoc para utilizar en un paquete único. Para crear este destino ODBC ad hoc, use el componente de script como se muestra en el ejemplo siguiente.  
  
> [!NOTE]  
>  Si desea crear un componente que pueda reutilizar más fácilmente en varias tareas de flujo de datos y varios paquetes, puede utilizar el código de este ejemplo de componente de script como punto de inicio para el componente de flujo de datos personalizado. Para obtener más información, vea [Desarrollar un componente de flujo de datos personalizado](../../integration-services/extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md).  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente se muestra cómo crear un componente de destino que usa un ODBC existente en el Administrador de conexiones para guardar los datos del flujo de datos en un [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabla.  
  
 En este ejemplo es una versión modificada de personalizado [!INCLUDE[vstecado](../../includes/vstecado-md.md)] destino que se muestra en el tema, [crear un destino con el componente de Script](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-destination-with-the-script-component.md). Sin embargo, en este ejemplo, el destino [!INCLUDE[vstecado](../../includes/vstecado-md.md)] personalizado se ha modificado para que funcione con un administrador de conexiones ODBC y guarde los datos a un destino de ODBC. Estas modificaciones también incluyen los cambios siguientes:  
  
-   No se puede llamar el **AcquireConnection** método del Administrador de conexiones ODBC desde código administrado, porque devuelve un objeto nativo. Por consiguiente, este ejemplo usa la cadena de conexión del administrador de conexiones para conectar directamente al origen de datos mediante el proveedor de datos de [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] para ODBC administrado.  
  
-   El **con OdbcCommand** espera parámetros posicionales. Los signos de interrogación (?) en el texto del comando indican las posiciones de los parámetros. (En cambio, un **SqlCommand** espera parámetros con nombre.)  
  
 Este ejemplo se utiliza la **Person.Address** tabla el **AdventureWorks** base de datos de ejemplo. En el ejemplo se pasa la primera y cuarta columna, la  **int*AddressID*** y **nvarchar (30) Ciudad** columnas de esta tabla a través del flujo de datos. Estos mismos datos se utilizan en el origen, transformación y ejemplos de destino en el tema [desarrollar específico Types of Script Components](../../integration-services/extending-packages-scripting-data-flow-script-component-types/developing-specific-types-of-script-components.md).  
  
#### <a name="to-configure-this-script-component-example"></a>Para configurar este ejemplo de componente de script  
  
1.  Crear una conexión ODBC el administrador que se conecta a la **AdventureWorks** base de datos.  
  
2.  Cree una tabla de destino ejecutando el siguiente comando de Transact-SQL en el **AdventureWorks** base de datos:  
  
    ```sql
    CREATE TABLE [Person].[Address2]([AddressID] [int] NOT NULL,  
        [City] [nvarchar](30) NOT NULL)  
    ```  
  
3.  Agregue un nuevo componente de script a la superficie del diseñador de flujo de datos y configúrelo como destino.  
  
4.  Conecte la salida de un origen o transformación de nivel superior al componente de destino en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)]. (Puede conectar directamente un origen a un destino sin ninguna transformación.) Para asegurarse de que funciona este ejemplo, la salida del componente de nivel superior debe incluir al menos la **AddressID** y **City** columnas de la **Person.Address** tabla de la **AdventureWorks** base de datos de ejemplo.  
  
5.  Abra la **Editor de transformación Script**. En el **columnas de entrada** página, seleccione la **AddressID** y **City** columnas.  
  
6.  En el **entradas y salidas** página, cambie el nombre de la entrada con un nombre más descriptivo como **MyAddressInput**.  
  
7.  En el **administradores de conexión** página, agregue o cree la conexión ODBC Administrador con un nombre descriptivo como **MyODBCConnectionManager**.  
  
8.  En el **Script** página, haga clic en **editar Script**y, a continuación, escriba el script se muestra a continuación, en la **ScriptMain** clase.  
  
9. Cierre el entorno de desarrollo de script, cierre el **Editor de transformación Script**, y, a continuación, ejecutar el ejemplo.  
  
    ```vb  
    Imports System.Data.Odbc  
    ...  
    Public Class ScriptMain  
        Inherits UserComponent  
  
        Dim odbcConn As OdbcConnection  
        Dim odbcCmd As OdbcCommand  
        Dim odbcParam As OdbcParameter  
  
        Public Overrides Sub AcquireConnections(ByVal Transaction As Object)  
  
            Dim connectionString As String  
            connectionString = Me.Connections.MyODBCConnectionManager.ConnectionString  
            odbcConn = New OdbcConnection(connectionString)  
            odbcConn.Open()  
  
        End Sub  
  
        Public Overrides Sub PreExecute()  
  
            odbcCmd = New OdbcCommand("INSERT INTO Person.Address2(AddressID, City) " & _  
                "VALUES(?, ?)", odbcConn)  
            odbcParam = New OdbcParameter("@addressid", OdbcType.Int)  
            odbcCmd.Parameters.Add(odbcParam)  
            odbcParam = New OdbcParameter("@city", OdbcType.NVarChar, 30)  
            odbcCmd.Parameters.Add(odbcParam)  
  
        End Sub  
  
        Public Overrides Sub MyAddressInput_ProcessInputRow(ByVal Row As MyAddressInputBuffer)  
  
            With odbcCmd  
                .Parameters("@addressid").Value = Row.AddressID  
                .Parameters("@city").Value = Row.City  
                .ExecuteNonQuery()  
            End With  
  
        End Sub  
  
        Public Overrides Sub ReleaseConnections()  
  
            odbcConn.Close()  
  
        End Sub  
  
    End Class  
    ```  
  
    ```csharp  
    using System.Data.Odbc;  
    ...  
    public class ScriptMain :  
        UserComponent  
    {  
        OdbcConnection odbcConn;  
        OdbcCommand odbcCmd;  
        OdbcParameter odbcParam;  
  
        public override void AcquireConnections(object Transaction)  
        {  
  
            string connectionString;  
            connectionString = this.Connections.MyODBCConnectionManager.ConnectionString;  
            odbcConn = new OdbcConnection(connectionString);  
            odbcConn.Open();  
  
        }  
  
        public override void PreExecute()  
        {  
  
            odbcCmd = new OdbcCommand("INSERT INTO Person.Address2(AddressID, City) " +  
                "VALUES(?, ?)", odbcConn);  
            odbcParam = new OdbcParameter("@addressid", OdbcType.Int);  
            odbcCmd.Parameters.Add(odbcParam);  
            odbcParam = new OdbcParameter("@city", OdbcType.NVarChar, 30);  
            odbcCmd.Parameters.Add(odbcParam);  
  
        }  
  
        public override void MyAddressInput_ProcessInputRow(MyAddressInputBuffer Row)  
        {  
  
            {  
                odbcCmd.Parameters["@addressid"].Value = Row.AddressID;  
                odbcCmd.Parameters["@city"].Value = Row.City;  
                odbcCmd.ExecuteNonQuery();  
            }  
  
        }  
  
        public override void ReleaseConnections()  
        {  
  
            odbcConn.Close();  
  
        }  
    }  
    ```  
  
## <a name="see-also"></a>Vea también  
 [Crear un destino con el componente de script](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-destination-with-the-script-component.md)  
  
  

