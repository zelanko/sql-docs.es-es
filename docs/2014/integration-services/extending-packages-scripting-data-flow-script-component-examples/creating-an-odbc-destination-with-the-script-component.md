---
title: Crear un destino ODBC con el componente de script | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- Script component [Integration Services], destination components
- ODBC destination [Integration Services]
- destinations [Integration Services], components
- Script component [Integration Services], examples
ms.assetid: d198c866-78f4-4a50-ae15-333160645815
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: e3049839f14d25413cee64ced2340578c178d6bb
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/13/2018
ms.locfileid: "53356290"
---
# <a name="creating-an-odbc-destination-with-the-script-component"></a>Crear un destino ODBC con el componente de script
  En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], normalmente se guardan los datos en un destino ODBC mediante un destino [!INCLUDE[vstecado](../../includes/vstecado-md.md)] y el proveedor de datos de [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] para ODBC. Sin embargo, también se puede crear un destino ODBC ad hoc para utilizar en un paquete único. Para crear este destino ODBC ad hoc, use el componente de script como se muestra en el ejemplo siguiente.  
  
> [!NOTE]  
>  Si desea crear un componente que pueda reutilizar más fácilmente en varias tareas de flujo de datos y varios paquetes, puede utilizar el código de este ejemplo de componente de script como punto de inicio para el componente de flujo de datos personalizado. Para obtener más información, vea [Desarrollar un componente de flujo de datos personalizado](../extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md).  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente se muestra cómo crear un componente de destino que usa un administrador de conexiones ODBC existente para guardar los datos del flujo de datos en una tabla de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Este ejemplo es una versión modificada del destino [!INCLUDE[vstecado](../../includes/vstecado-md.md)] personalizado que se mostró en el tema [Crear un destino con el componente de script](../extending-packages-scripting-data-flow-script-component-types/creating-a-destination-with-the-script-component.md). Sin embargo, en este ejemplo, el destino [!INCLUDE[vstecado](../../includes/vstecado-md.md)] personalizado se ha modificado para que funcione con un administrador de conexiones ODBC y guarde los datos a un destino de ODBC. Estas modificaciones también incluyen los cambios siguientes:  
  
-   No puede llamar al método `AcquireConnection` del administrador de conexiones ODBC desde el código administrado, porque devuelve un objeto nativo. Por consiguiente, este ejemplo usa la cadena de conexión del administrador de conexiones para conectar directamente al origen de datos mediante el proveedor de datos de [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] para ODBC administrado.  
  
-   `OdbcCommand` espera los parámetros posicionales. Los signos de interrogación (?) en el texto del comando indican las posiciones de los parámetros. (En cambio, `SqlCommand` espera parámetros con nombre.)  
  
 En este ejemplo se usa la tabla **Person.Address** en la base de datos de ejemplo **AdventureWorks**. En el ejemplo se pasan las columnas primera y cuarta, las columnas **int*AddressID*** y **nvarchar(30)City**, de esta tabla a través del flujo de datos. Estos mismos datos se usan en los ejemplos de origen, transformación y destino en el tema [Desarrollar tipos específicos de los componentes de script](../extending-packages-scripting-data-flow-script-component-types/developing-specific-types-of-script-components.md).  
  
#### <a name="to-configure-this-script-component-example"></a>Para configurar este ejemplo de componente de script  
  
1.  Cree un administrador de conexiones ODBC que se conecte a la base de datos **AdventureWorks**.  
  
2.  Cree una tabla de destino ejecutando el siguiente comando Transact-SQL en la base de datos **AdventureWorks**:  
  
    ```  
    CREATE TABLE [Person].[Address2]([AddressID] [int] NOT NULL,  
        [City] [nvarchar](30) NOT NULL)  
    ```  
  
3.  Agregue un nuevo componente de script a la superficie del diseñador de flujo de datos y configúrelo como destino.  
  
4.  Conecte la salida de un origen o transformación de nivel superior al componente de destino en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)]. (Puede conectar directamente un origen a un destino sin ninguna transformación.) Para asegurarse de que este ejemplo funciona, la salida del componente ascendente debe incluir por lo menos las columnas **AddressID** y **City** de la tabla **Person.Address** de la base de datos de ejemplo **AdventureWorks**.  
  
5.  Abra el **Editor de transformación Script**. En la página **Columnas de entrada**, seleccione las columnas **AddressID** y **City**.  
  
6.  En la página **Entradas y salidas**, cambie el nombre de la entrada por un nombre más descriptivo, como **MyAddressInput**.  
  
7.  En la página **Administradores de conexiones**, agregue o cree el administrador de conexiones ODBC con un nombre descriptivo, como **MyODBCConnectionManager**.  
  
8.  En el **Script** página, haga clic en **editar Script**y, a continuación, escriba el script se muestra a continuación, en la `ScriptMain` clase.  
  
9. Cierre el entorno de desarrollo de script y el **Editor de transformación Script** y, a continuación, ejecute el ejemplo.  
  
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
  
![Icono de Integration Services (pequeño)](../media/dts-16.gif "icono de Integration Services (pequeño)")**mantenerse actualizado con Integration Services**<br /> Para obtener las descargas, artículos, ejemplos y vídeos más recientes de Microsoft, así como soluciones seleccionadas de la comunidad, visite la página de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] en MSDN:<br /><br /> [Visite la página de Integration Services en MSDN](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Para recibir notificaciones automáticas de estas actualizaciones, suscríbase a las fuentes RSS disponibles en la página.  
  
## <a name="see-also"></a>Vea también  
 [Crear un destino con el componente de script](../extending-packages-scripting-data-flow-script-component-types/creating-a-destination-with-the-script-component.md)  
  
  
