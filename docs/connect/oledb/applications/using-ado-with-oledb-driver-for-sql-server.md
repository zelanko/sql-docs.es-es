---
title: Uso de ADO con el controlador OLE DB para SQL Server | Microsoft Docs
description: Uso de ADO con el controlador OLE DB para SQL Server
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, ADO
- data access [OLE DB Driver for SQL Server], ADO
- ADO [OLE DB Driver for SQL Server]
- MSOLEDBSQL, ADO
author: pmasl
ms.author: pelopes
manager: jroth
ms.openlocfilehash: 1906ad25e9bb170b8979f44757ec5742ad9ec6c4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66778049"
---
# <a name="using-ado-with-ole-db-driver-for-sql-server"></a>Uso de ADO con el controlador OLE DB para SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Para aprovechar las características nuevas introducidas en [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], como los conjuntos de resultados activos múltiples (MARS), las notificaciones de consulta, los tipos definidos por el usuario (UDT) o el nuevo tipo de datos **xml**, las aplicaciones existentes que usan Objetos de datos ActiveX (ADO) deberían usar el controlador OLE DB para SQL Server como su proveedor de acceso a datos.  
  
 Para permitir que ADO use las características nuevas de las versiones más recientes de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], se han realizado algunas mejoras en el controlador OLE DB para SQL Server que extiende las características principales de OLE DB. Estas mejoras permiten a las aplicaciones ADO usar las características más recientes de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] y usar dos tipos de datos introducidos en [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]: **xml** y **udt**. Estas mejoras también aprovechan las mejoras realizadas en los tipos de datos **varchar**, **nvarchar** y **varbinary**. El controlador OLE DB para SQL Server agrega la propiedad de inicialización SSPROP_INIT_DATATYPECOMPATIBILITY al conjunto de propiedades DBPROPSET_SQLSERVERDBINIT para que las aplicaciones ADO la usen de modo que los nuevos tipos de datos se expongan de un modo compatible con ADO. Además, el controlador OLE DB para SQL Server también define una nueva palabra clave de conexión denominada **DataTypeCompatibility** que se establece en la cadena de conexión.  

> [!NOTE]  
>  Las aplicaciones ADO existentes pueden obtener acceso y actualizar XML, UDT, texto de valores grandes y valores de campo binarios mediante el proveedor SQLOLEDB. Los nuevos tipos de datos de mayor tamaño **varchar(max)** , **nvarchar(max)** y **varbinary(max)** se devuelven como los tipos ADO **adLongVarChar**, **adLongVarWChar** y **adLongVarBinary** respectivamente. Las columnas XML se devuelven como **adLongVarChar** y las columnas UDT se devuelven como **adVarBinary**. Sin embargo, si usa el controlador OLE DB para SQL Server (MSOLEDBSQL) en lugar de SQLOLEDB, debe asegurarse de establecer el **DataTypeCompatibility** palabra clave en "80" para que los nuevos tipos de datos se asignen correctamente a los tipos de datos de ADO.  

## <a name="enabling-ole-db-driver-for-sql-server-from-ado"></a>Habilitar el controlador OLE DB para SQL Server de ADO  
 Para habilitar el uso del controlador OLE DB para SQL Server, las aplicaciones ADO necesitarán implementar las siguientes palabras clave en sus cadenas de conexión:  

-   `Provider=MSOLEDBSQL`  

-   `DataTypeCompatibility=80`  

 Para más información sobre las palabras clave de cadena de conexión de ADO compatibles en el controlador OLE DB para SQL Server, vea [Uso de palabras clave de cadena de conexión con el controlador OLE DB para SQL Server](../../oledb/applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md).  

 A continuación se muestra un ejemplo sobre la forma de establecer una cadena de conexión de ADO totalmente habilitada para funcionar con el controlador OLE DB para SQL Server, así como la forma de habilitar la característica MARS:  

```  
Dim con As New ADODB.Connection  

con.ConnectionString = "Provider=MSOLEDBSQL;" _  
         & "Server=(local);" _  
         & "Database=AdventureWorks;" _   
         & "Integrated Security=SSPI;" _  
         & "DataTypeCompatibility=80;" _  
         & "MARS Connection=True;"  
con.Open  
```  

## <a name="examples"></a>Ejemplos  
 Las secciones siguientes proporcionan ejemplos de cómo usar ADO con el controlador OLE DB para SQL Server.  

### <a name="retrieving-xml-column-data"></a>Recuperar datos de columna XML  
 En este ejemplo, se usa un conjunto de registros para recuperar y mostrar los datos de una columna XML en la base de datos de ejemplo **AdventureWorks** de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  

```  
Dim con As New ADODB.Connection  
Dim rst As New ADODB.Recordset  
Dim sXMLResult As String  

con.ConnectionString = "Provider=MSOLEDBSQL;" _  
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
 En este ejemplo, se usa un objeto **Command** para ejecutar una consulta SQL que devuelve un UDT, los datos del UDT se actualizan y, después, los nuevos datos vuelven a insertarse en la base de datos. En este ejemplo, se asume que el UDT **Point** ya se ha registrado en la base de datos.  

```  
Dim con As New ADODB.Connection  
Dim cmd As New ADODB.Command  
Dim rst As New ADODB.Recordset  
Dim strOldUDT As String  
Dim strNewUDT As String  
Dim aryTempUDT() As String  
Dim strTempID As String  
Dim i As Integer  

con.ConnectionString = "Provider=MSOLEDBSQL;" _  
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
 En este ejemplo, se crea una cadena de conexión para habilitar MARS a través del controlador OLE DB para SQL Server y, después, se crean dos objetos de conjunto de registros para ejecutarlos mediante la misma conexión.  

```  
Dim con As New ADODB.Connection  

con.ConnectionString = "Provider=MSOLEDBSQL;" _  
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

 En versiones anteriores del proveedor OLE DB, este código hacía que se crease una conexión implícita en la segunda ejecución porque solo podía abrirse un conjunto de resultados activo por cada conexión única. Dado que la conexión implícita no estaba agrupada en el grupo de conexiones OLE DB, esto produciría una sobrecarga adicional. Con la característica MARS expuesta por el controlador OLE DB para SQL Server, se obtienen varios resultados activos en la conexión única.  

## <a name="see-also"></a>Consulte también  
 [Compilación de aplicaciones con el controlador OLE DB para SQL Server](../../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)  
