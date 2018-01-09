---
title: Las funciones con valores escalares CLR | Documentos de Microsoft
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: clr
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
dev_langs:
- TSQL
- VB
- CSharp
helpviewer_keywords:
- SVF
- scalar-valued functions
ms.assetid: 20dcf802-c27d-4722-9cd3-206b1e77bee0
caps.latest.revision: "81"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 31dcc25d371ee74d69af1f7a85ad34208d99fd79
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/08/2018
---
# <a name="clr-scalar-valued-functions"></a>Funciones escalares de CLR
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]Una función escalar (SVF) devuelve un valor único, como una cadena, entero o un valor de bit. Puede crear funciones definidas por el usuario escalares en código administrado mediante cualquier lenguaje de programación de .NET Framework. Estas funciones son accesibles para [!INCLUDE[tsql](../../includes/tsql-md.md)] u otro código administrado. Para obtener información acerca de las ventajas de la integración de CLR y elegir entre código administrado y [!INCLUDE[tsql](../../includes/tsql-md.md)], consulte [información general de la integración CLR](../../relational-databases/clr-integration/clr-integration-overview.md).  
  
## <a name="requirements-for-clr-scalar-valued-functions"></a>Requisitos de las funciones escalares de CLR  
 Las SVF de .NET Framework se implementan como métodos en una clase de un ensamblado de .NET Framework. Los parámetros de entrada y el tipo devuelto de una SVF pueden ser cualquiera de los tipos de datos escalares admitidos por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], excepto **varchar**, **char**, **rowversion**, **texto**, **ntext**, **imagen**, **timestamp**, **tabla**, o **cursor** . Las SVF deben asegurar una coincidencia entre el tipo de datos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y el tipo de datos de retorno del método de implementación. Para obtener más información acerca de las conversiones de tipo, consulte [asignación de datos de parámetro de CLR](../../relational-databases/clr-integration-database-objects-types-net-framework/mapping-clr-parameter-data.md).  
  
 Al implementar una SVF de .NET Framework SVF en un lenguaje .NET Framework, el atributo personalizado **SqlFunction** se puede especificar para incluir la información adicional de la función. El atributo **SqlFunction** indica tanto si la función obtiene acceso o modifica los datos como si no, si es determinista y si la función implica las operaciones de coma flotante.  
  
 Las funciones escalares definidas por el usuario pueden ser deterministas o no deterministas. Una función determinista siempre devuelve el mismo resultado cuando se llama con un conjunto concreto de parámetros de entrada. Una función no determinista puede devolver resultados distintos cuando se llama con un conjunto concreto de parámetros de entrada.  
  
> [!NOTE]  
>  No marque una función como determinista si ésta no siempre genera los mismos valores de salida, dados los mismos valores de entrada y el mismo estado de la base de datos. Al marcar una función como determinista cuando la función no es verdaderamente determinista puede producir vistas indizadas dañadas y columnas calculadas. Marque una función como determinista estableciendo la propiedad **IsDeterministic** en true.  
  
### <a name="table-valued-parameters"></a>Parámetros con valores de tabla  
 Los parámetros con valores de tabla (TVP), tipos de tabla definidos por el usuario que se pasan a un procedimiento o función, proporcionan un modo eficaz de pasar varias filas de datos al servidor. Los TVP presentan una funcionalidad similar a las matrices de parámetros, pero proporcionan más flexibilidad y una mayor integración con [!INCLUDE[tsql](../../includes/tsql-md.md)]. También proporcionan la posibilidad de obtener mayor rendimiento. Además, los TVP ayudan a reducir el número de ciclos de ida y vuelta al servidor. En lugar de enviar varias solicitudes al servidor, como con una lista de parámetros escalares, los datos pueden enviarse al servidor como un TVP. Un tipo de tabla definido por el usuario no puede pasarse como un parámetro con valores de tabla a un procedimiento almacenado administrado o a una función que se ejecuta en el proceso de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], así como tampoco puede devolverse desde dicho procedimiento o función. Para obtener más información acerca de Tvp, vea [usar parámetros &#40; motor de base de datos &#41;](../../relational-databases/tables/use-table-valued-parameters-database-engine.md).  
  
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
  
 La primera línea de código hace referencia a **Microsoft.SqlServer.Server** para tener acceso a los atributos y a **System.Data.SqlClient** para tener acceso al espacio de nombres de ADO.NET. (Este espacio de nombres contiene **SqlClient**, el proveedor de datos de .NET Framework para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].)  
  
 Después, la función recibe el atributo personalizado **SqlFunction** , que se encuentra en el espacio de nombres **Microsoft.SqlServer.Server** . El atributo personalizado indica si la función definida por el usuario (UDF) utiliza o no el proveedor en proceso para leer los datos en el servidor. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no permite a las UDF actualizar, insertar o eliminar datos. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] puede optimizar la ejecución de una UDF que no usa el proveedor en proceso. Esto se indica estableciendo **DataAccessKind** en **DataAccessKind.None**. En la línea siguiente, el método de destino es una estática pública (se comparte en Visual Basic .NET).  
  
 El **SqlContext** (clase), ubicado en el **Microsoft.SqlServer.Server** espacio de nombres, a continuación, puede tener acceso a un **SqlCommand** objeto con una conexión a la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instancia que ya está configurado. Aunque no se usa aquí, el contexto de transacción actual también está disponible a través de la interfaz de programación de aplicaciones (API) **System.Transactions** .  
  
 Los desarrolladores que han escrito las aplicaciones cliente que usan los tipos situados en el espacio de nombres **System.Data.SqlClient** , deberían estar familiarizados con la mayoría de las líneas de código en el cuerpo de la función.  
  
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
  
 El texto de comando adecuado se especifica inicializando el objeto **SqlCommand** . En el ejemplo anterior se cuenta el número de filas en la tabla **SalesOrderHeader**. Después, se llama al método **ExecuteScalar** del objeto **cmd** . Esto devuelve un valor de tipo **int** basado en la consulta. Por último, se devuelve Order Count al autor de la llamada.  
  
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
>  Objetos de base de datos de Visual C++ compilan con **/CLR: pure** no se admiten para la ejecución en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Por ejemplo, esos objetos de base de datos incluyen funciones escalares.  
  
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
 [La asignación de datos de parámetro CLR](../../relational-databases/clr-integration-database-objects-types-net-framework/mapping-clr-parameter-data.md)   
 [Información general de atributos personalizados de integración de CLR](http://msdn.microsoft.com/library/ecf5c097-0972-48e2-a9c0-b695b7dd2820)   
 [Funciones definidas por el usuario](../../relational-databases/user-defined-functions/user-defined-functions.md)   
 [Acceso a datos de objetos de base de datos de CLR](../../relational-databases/clr-integration/data-access/data-access-from-clr-database-objects.md)  
  
  
