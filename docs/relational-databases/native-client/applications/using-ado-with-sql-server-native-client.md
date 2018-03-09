---
title: Usar ADO con SQL Server Native Client | Documentos de Microsoft
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client|applications
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client, ADO
- data access [SQL Server Native Client], ADO
- ADO [SQL Server Native Client]
- SQLNCLI, ADO
ms.assetid: 118a7cac-4c0d-44fd-b63e-3d542932d239
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 13978b8eb01fda4b9478111a3bef3e36c76f8e58
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/25/2018
---
# <a name="using-ado-with-sql-server-native-client"></a>Usar ADO con SQL Server Native Client
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  Para aprovechar las nuevas características introducidas en [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] como conjuntos de resultados activos múltiples (MARS), las notificaciones de consulta, tipos definidos por el usuario (UDT) o el nuevo **xml** tipo de datos, las aplicaciones existentes que utilizan controles ActiveX Data Objects (ADO) debe usar el [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client como su proveedor de acceso a datos.  
  
 Si no necesita usar ninguna de las características nuevas introducidas en [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], no tiene necesidad de usar el proveedor OLE DB de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client; puede seguir usando su proveedor de acceso a datos actual, que suele ser SQLOLEDB. Si está mejorando una aplicación existente y necesita usar las características nuevas introducidas en [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], debería utilizar el proveedor OLE DB de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client.  
  
> [!NOTE]  
>  Si está desarrollando una nueva aplicación, es recomendable que considere la posibilidad de usar ADO.NET y el proveedor de datos de .NET Framework para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en lugar de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client a fin de obtener acceso a todas las características nuevas de las versiones más recientes de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Para obtener más información acerca del proveedor de datos de .NET Framework para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], vea la documentación de .NET Framework SDK para ADO.NET.  
  
 Para permitir que ADO utilice las características nuevas de las versiones más recientes de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], se han realizado algunas mejoras en el proveedor OLE DB de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client que extiende las características principales de OLE DB. Estas mejoras permiten a las aplicaciones ADO usar versiones más recientes [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] características y consumir dos tipos de datos introducidos en [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]: **xml** y **udt**. Estas mejoras también aprovechan las mejoras en el **varchar**, **nvarchar**, y **varbinary** tipos de datos. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client agrega la propiedad de inicialización SSPROP_INIT_DATATYPECOMPATIBILITY al conjunto de propiedades DBPROPSET_SQLSERVERDBINIT establecer para su uso por aplicaciones ADO, para que los nuevos tipos de datos se exponen en un modo compatible con ADO. Además, el [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client también define una nueva palabra clave de conexión denominada **DataTypeCompatibility** que se establece en la cadena de conexión.  
  
> [!NOTE]  
>  Las aplicaciones ADO existentes pueden obtener acceso y actualizar XML, UDT, texto de valores grandes y valores de campo binarios mediante el proveedor SQLOLEDB. El nuevo mayor **varchar (max)**, **nvarchar (max)**, y **varbinary (max)** tipos de datos se devuelven como los tipos ADO **adLongVarChar**, **adLongVarWChar** y **adLongVarBinary** respectivamente. Las columnas XML se devuelven como **adLongVarChar**, y las columnas UDT se devuelven como **adVarBinary**. Sin embargo, si usa el [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] el proveedor OLE DB de Native Client (SQLNCLI11) en lugar de SQLOLEDB, debe asegurarse de establecer la **DataTypeCompatibility** palabra clave en "80" para que los nuevos tipos de datos se asignen correctamente a los datos de ADO tipos.  
  
## <a name="enabling-sql-server-native-client-from-ado"></a>Habilitar SQL Server Native Client desde ADO  
 Para habilitar el uso de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, las aplicaciones ADO necesitarán implementar las siguientes palabras clave en sus cadenas de conexión:  
  
-   `Provider=SQLNCLI11`  
  
-   `DataTypeCompatibility=80`  
  
 Para obtener más información acerca de la propiedad ADO palabras clave que se admiten en la cadena de conexión [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, vea [Using Connection String Keywords with SQL Server Native Client](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md).  
  
 El siguiente es un ejemplo de establecimiento de una cadena de conexión de ADO totalmente habilitada para trabajar con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, incluida la habilitación de la característica MARS:  
  
```  
Dim con As New ADODB.Connection  
  
con.ConnectionString = "Provider=SQLNCLI11;" _  
         & "Server=(local);" _  
         & "Database=AdventureWorks;" _   
         & "Integrated Security=SSPI;" _  
         & "DataTypeCompatibility=80;" _  
         & "MARS Connection=True;"  
con.Open  
```  
  
## <a name="examples"></a>Ejemplos  
 Las secciones siguientes proporcionan ejemplos de cómo puede usar ADO con el [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] proveedor Native Client OLE DB.  
  
### <a name="retrieving-xml-column-data"></a>Recuperar datos de columna XML  
 En este ejemplo, un conjunto de registros se utiliza para recuperar y mostrar los datos de una columna XML en el [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **AdventureWorks** base de datos de ejemplo.  
  
```  
Dim con As New ADODB.Connection  
Dim rst As New ADODB.Recordset  
Dim sXMLResult As String  
  
con.ConnectionString = "Provider=SQLNCLI11;" _  
         & "Server=(local);" _  
         & "Database=AdventureWorks;" _   
         & "Integrated Security=SSPI;" _   
         & "DataTypeCompatibility=80;"  
  
con.Open  
  
' Get the xml data as a recordset.  
Set rst.ActiveConnection = con  
rst.Source = "SELECT AdditionalContactInfo FROM Person.Contact " _  
   & "WHERE AdditionalContactInfo IS NOT NULL"  
rst.Open  
  
' Display the data in the recordset.  
While (Not rst.EOF)  
   sXMLResult = rst.Fields("AdditionalContactInfo").Value  
   Debug.Print (sXMLResult)  
   rst.MoveNext  
End While  
  
con.Close  
Set con = Nothing  
```  
  
> [!NOTE]  
>  No se admite el filtrado de conjuntos de registros con columnas XML. Si se utiliza, se devolverá un error.  
  
### <a name="retrieving-udt-column-data"></a>Recuperar datos de columna UDT  
 En este ejemplo, un **comando** objeto se usa para ejecutar una consulta SQL que devuelve un UDT, se actualizan los datos UDT y, a continuación, los nuevos datos vuelven a insertarse en la base de datos. En este ejemplo se da por supuesto que el **punto** UDT ya se ha registrado en la base de datos.  
  
```  
Dim con As New ADODB.Connection  
Dim cmd As New ADODB.Command  
Dim rst As New ADODB.Recordset  
Dim strOldUDT As String  
Dim strNewUDT As String  
Dim aryTempUDT() As String  
Dim strTempID As String  
Dim i As Integer  
  
con.ConnectionString = "Provider=SQLNCLI11;" _  
         & "Server=(local);" _  
         & "Database=AdventureWorks;" _   
         & "Integrated Security=SSPI;" _  
         & "DataTypeCompatibility=80;"  
  
con.Open  
  
' Get the UDT value.  
Set cmd.ActiveConnection = con  
cmd.CommandText = "SELECT ID, Pnt FROM dbo.Points.ToString()"  
Set rst = cmd.Execute  
strTempID = rst.Fields(0).Value  
strOldUDT = rst.Fields(1).Value  
  
' Do something with the UDT by adding i to each point.  
arytempUDT = Split(strOldUDT, ",")  
i = 3  
strNewUDT = LTrim(Str(Int(aryTempUDT(0)) + i)) + "," + _  
   LTrim(Str(Int(aryTempUDT(1)) + i))  
  
' Insert the new value back into the database.  
cmd.CommandText = "UPDATE dbo.Points SET Pnt = '" + strNewUDT + _  
   "' WHERE ID = '" + strTempID + "'"  
cmd.Execute  
  
con.Close  
Set con = Nothing  
```  
  
### <a name="enabling-and-using-mars"></a>Habilitar y utilizar MARS  
 En este ejemplo, se construye la cadena de conexión para habilitar MARS a través de la [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] proveedor Native Client OLE DB y, a continuación, dos objetos de conjunto de registros se crean para ejecutar mediante la misma conexión.  
  
```  
Dim con As New ADODB.Connection  
  
con.ConnectionString = "Provider=SQLNCLI11;" _  
         & "Server=(local);" _  
         & "Database=AdventureWorks;" _   
         & "Integrated Security=SSPI;" _  
         & "DataTypeCompatibility=80;" _  
         & "MARS Connection=True;"  
con.Open  
  
Dim recordset1 As New ADODB.Recordset  
Dim recordset2 As New ADODB.Recordset  
  
Dim recordsaffected As Integer  
Set recordset1 =  con.Execute("SELECT * FROM Table1", recordsaffected, adCmdText)  
Set recordset2 =  con.Execute("SELECT * FROM Table2", recordsaffected, adCmdText)  
  
con.Close  
Set con = Nothing  
```  
  
 En versiones anteriores del proveedor OLE DB, este código hacía que se crease una conexión implícita en la segunda ejecución porque solo podía abrirse un conjunto de resultados activo por cada conexión única. Dado que la conexión implícita no estaba agrupada en el grupo de conexiones OLE DB, esto produciría una sobrecarga adicional. Con la característica MARS expuesta por el [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client, se obtienen varios resultados activos en una conexión.  
  
## <a name="see-also"></a>Vea también  
 [Creación de aplicaciones con SQL Server Native Client](../../../relational-databases/native-client/applications/building-applications-with-sql-server-native-client.md)  
  
  
