---
title: Las funciones con valores escalares CLR | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
dev_langs:
- TSQL
- VB
- CSharp
helpviewer_keywords:
- SVF
- scalar-valued functions
ms.assetid: 20dcf802-c27d-4722-9cd3-206b1e77bee0
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: cf5c0b6c7004f458e424e58d738cce22e97afa2b
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48157365"
---
# <a name="clr-scalar-valued-functions"></a>Funciones escalares de CLR
  Una función escalar (SVF) devuelve un único valor, como un valor de cadena, entero o de bit. Puede crear funciones escalares definidas por el usuario en código administrado mediante cualquier lenguaje de programación de .NET Framework. Estas funciones son accesibles para [!INCLUDE[tsql](../../includes/tsql-md.md)] u otro código administrado. Para obtener información acerca de las ventajas de la integración de CLR y elegir entre código administrado y [!INCLUDE[tsql](../../includes/tsql-md.md)], consulte [información general de la integración CLR](../clr-integration/clr-integration-overview.md).  
  
## <a name="requirements-for-clr-scalar-valued-functions"></a>Requisitos de las funciones escalares de CLR  
 Las SVF de .NET Framework se implementan como métodos en una clase de un ensamblado de .NET Framework. Los parámetros de entrada y el tipo devuelto de una SVF pueden ser cualquiera de los tipos de datos escalares admitidos por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], excepto `varchar`, `char`, `rowversion`, `text`, `ntext`, `image`, `timestamp`, `table`, o `cursor`. Las SVF deben asegurar una coincidencia entre el tipo de datos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y el tipo de datos de retorno del método de implementación. Para obtener más información sobre las conversiones de tipos, vea [asignación de datos de parámetros CLR](../clr-integration-database-objects-types-net-framework/mapping-clr-parameter-data.md).  
  
 Al implementar una SVF de .NET Framework SVF en un lenguaje .NET Framework, el atributo personalizado `SqlFunction` se puede especificar para incluir la información adicional de la función. El atributo `SqlFunction` indica tanto si la función obtiene acceso o modifica los datos como si no, si es determinista y si la función implica las operaciones de coma flotante.  
  
 Las funciones escalares definidas por el usuario pueden ser deterministas o no deterministas. Una función determinista siempre devuelve el mismo resultado cuando se llama con un conjunto concreto de parámetros de entrada. Una función no determinista puede devolver resultados distintos cuando se llama con un conjunto concreto de parámetros de entrada.  
  
> [!NOTE]  
>  No marque una función como determinista si ésta no siempre genera los mismos valores de salida, dados los mismos valores de entrada y el mismo estado de la base de datos. Al marcar una función como determinista cuando la función no es verdaderamente determinista puede producir vistas indizadas dañadas y columnas calculadas. Marque una función como determinista estableciendo la propiedad `IsDeterministic` en true.  
  
### <a name="table-valued-parameters"></a>Parámetros con valores de tabla  
 Los parámetros con valores de tabla (TVP), tipos de tabla definidos por el usuario que se pasan a un procedimiento o función, proporcionan un modo eficaz de pasar varias filas de datos al servidor. Los TVP presentan una funcionalidad similar a las matrices de parámetros, pero proporcionan más flexibilidad y una mayor integración con [!INCLUDE[tsql](../../includes/tsql-md.md)]. También proporcionan la posibilidad de obtener mayor rendimiento. Además, los TVP ayudan a reducir el número de ciclos de ida y vuelta al servidor. En lugar de enviar varias solicitudes al servidor, como con una lista de parámetros escalares, los datos pueden enviarse al servidor como un TVP. Un tipo de tabla definido por el usuario no puede pasarse como un parámetro con valores de tabla a un procedimiento almacenado administrado o a una función que se ejecuta en el proceso de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], así como tampoco puede devolverse desde dicho procedimiento o función. Para obtener más información acerca de Tvp, vea [usar parámetros &#40;motor de base de datos&#41;](../tables/use-table-valued-parameters-database-engine.md).  
  
## <a name="example-of-a-clr-scalar-valued-function"></a>Ejemplo de una función escalar de CLR  
 A continuación se muestra una SVF simple que tiene acceso a datos y devuelve un valor entero:  
  
```csharp  
using Microsoft.SqlServer.Server;  
using System.Data.SqlClient;  
  
public class T  
{  
    [SqlFunction(DataAccess = DataAccessKind.Read)]  
    public static int ReturnOrderCount()  
    {  
        using (SqlConnection conn   
            = new SqlConnection("context connection=true"))  
        {  
            conn.Open();  
            SqlCommand cmd = new SqlCommand(  
                "SELECT COUNT(*) AS 'Order Count' FROM SalesOrderHeader", conn);  
            return (int)cmd.ExecuteScalar();  
        }  
    }  
}  
```  
  
```vb  
Imports Microsoft.SqlServer.Server  
Imports System.Data.SqlClient  
  
Public Class T  
    <SqlFunction(DataAccess:=DataAccessKind.Read)> _  
    Public Shared Function ReturnOrderCount() As Integer  
        Using conn As New SqlConnection("context connection=true")  
            conn.Open()  
            Dim cmd As New SqlCommand("SELECT COUNT(*) AS 'Order Count' FROM SalesOrderHeader", conn)  
            Return CType(cmd.ExecuteScalar(), Integer)  
        End Using  
    End Function  
End Class  
```  
  
 La primera línea de código hace referencia a `Microsoft.SqlServer.Server` para tener acceso a los atributos y a `System.Data.SqlClient` para tener acceso al espacio de nombres de ADO.NET. (Este espacio de nombres contiene `SqlClient`, el proveedor de datos de .NET Framework para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].)  
  
 Después, la función recibe el atributo personalizado `SqlFunction`, que se encuentra en el espacio de nombres `Microsoft.SqlServer.Server`. El atributo personalizado indica si la función definida por el usuario (UDF) utiliza o no el proveedor en proceso para leer los datos en el servidor. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no permite a las UDF actualizar, insertar o eliminar datos. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] puede optimizar la ejecución de una UDF que no usa el proveedor en proceso. Esto se indica estableciendo `DataAccessKind` en `DataAccessKind.None`. En la línea siguiente, el método de destino es una estática pública (se comparte en Visual Basic .NET).  
  
 La clase `SqlContext`, ubicada en el espacio de nombres `Microsoft.SqlServer.Server`, puede tener acceso a un objeto `SqlCommand` con una conexión a la instancia [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que ya está establecida. Aunque no se usa aquí, el contexto de transacción actual también está disponible a través de la interfaz de programación de aplicaciones (API) `System.Transactions`.  
  
 Los desarrolladores que han escrito las aplicaciones cliente que usan los tipos situados en el espacio de nombres `System.Data.SqlClient`, deberían estar familiarizados con la mayoría de las líneas de código en el cuerpo de la función.  
  
 [C#]  
  
```  
using(SqlConnection conn = new SqlConnection("context connection=true"))   
{  
   conn.Open();  
   SqlCommand cmd = new SqlCommand(  
        "SELECT COUNT(*) AS 'Order Count' FROM SalesOrderHeader", conn);  
   return (int) cmd.ExecuteScalar();  
}    
```  
  
 [Visual Basic]  
  
```  
Using conn As New SqlConnection("context connection=true")  
   conn.Open()  
   Dim cmd As New SqlCommand( _  
        "SELECT COUNT(*) AS 'Order Count' FROM SalesOrderHeader", conn)  
   Return CType(cmd.ExecuteScalar(), Integer)  
End Using  
```  
  
 El texto de comando adecuado se especifica inicializando el objeto `SqlCommand`. En el ejemplo anterior se cuenta el número de filas en la tabla `SalesOrderHeader`. Después, se llama al método `ExecuteScalar` del objeto `cmd`. Esto devuelve un valor de tipo `int` basado en la consulta. Por último, se devuelve Order Count al autor de la llamada.  
  
 Si este código se guarda en un archivo denominado FirstUdf.cs, puede estar compilado en un ensamblado como se muestra a continuación:  
  
 [C#]  
  
```  
csc.exe /t:library /out:FirstUdf.dll FirstUdf.cs   
```  
  
 [Visual Basic]  
  
```  
vbc.exe /t:library /out:FirstUdf.dll FirstUdf.vb  
```  
  
> [!NOTE]  
>  `/t:library` indica que se debe generar una biblioteca, en lugar de un ejecutable. Los ejecutables no se pueden registrar en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  Los objetos de base de datos de Visual C++ compilados con `/clr:pure` no se admiten para la ejecución en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Por ejemplo, esos objetos de base de datos incluyen funciones escalares.  
  
 La consulta [!INCLUDE[tsql](../../includes/tsql-md.md)] y una invocación de ejemplo para registrar el ensamblado y una UDF son:  
  
```  
CREATE ASSEMBLY FirstUdf FROM 'FirstUdf.dll';  
GO  
  
CREATE FUNCTION CountSalesOrderHeader() RETURNS INT   
AS EXTERNAL NAME FirstUdf.T.ReturnOrderCount;   
GO  
  
SELECT dbo.CountSalesOrderHeader();  
GO  
  
```  
  
 Observe que el nombre de función expuesto en [!INCLUDE[tsql](../../includes/tsql-md.md)] no necesita coincidir con el nombre del método estático público de destino.  
  
## <a name="see-also"></a>Vea también  
 [Asignar datos de parámetros CLR](../clr-integration-database-objects-types-net-framework/mapping-clr-parameter-data.md)   
 [Información general de atributos personalizados de integración de CLR](../../database-engine/dev-guide/overview-of-clr-integration-custom-attributes.md)   
 [Funciones definidas por el usuario](../user-defined-functions/user-defined-functions.md)   
 [Acceso a datos de objetos de base de datos de CLR](../clr-integration/data-access/data-access-from-clr-database-objects.md)  
  
  
