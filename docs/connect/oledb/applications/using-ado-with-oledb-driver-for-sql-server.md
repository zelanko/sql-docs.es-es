---
title: Usar ADO con controlador OLE DB para SQL Server | Documentos de Microsoft
description: Usar ADO con controlador OLE DB para SQL Server
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: oledb|applications
ms.reviewer: ''
ms.suite: sql
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, ADO
- data access [OLE DB Driver for SQL Server], ADO
- ADO [OLE DB Driver for SQL Server]
- MSOLEDBSQL, ADO
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 31dfd17d0e5f12cfddf88030e2b3516ea3ada0e6
ms.sourcegitcommit: 9f4330a4b067deea396b8567747a6771f35e6eee
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/30/2018
---
# <a name="using-ado-with-ole-db-driver-for-sql-server"></a>Usar ADO con controlador OLE DB para SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Para aprovechar las nuevas características introducidas en [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] como conjuntos de resultados activos múltiples (MARS), las notificaciones de consulta, tipos definidos por el usuario (UDT) o el nuevo **xml** tipo de datos, las aplicaciones existentes que utilizan controles ActiveX Data Objects (ADO) debe usar el controlador OLE DB para SQL Server como su proveedor de acceso a datos.  
  
 Para permitir que ADO usar las nuevas características de las versiones recientes de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], entre las mejoras se realizaron en el controlador OLE DB para SQL Server que amplía las características principales de OLE DB. Estas mejoras permiten a las aplicaciones ADO usar versiones más recientes [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] características y consumir dos tipos de datos introducidos en [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]: **xml** y **udt**. Estas mejoras también aprovechan las mejoras en el **varchar**, **nvarchar**, y **varbinary** tipos de datos. Controlador de OLE DB para SQL Server agrega la propiedad de inicialización SSPROP_INIT_DATATYPECOMPATIBILITY a la propiedad DBPROPSET_SQLSERVERDBINIT configurada para usarse en aplicaciones ADO, para que los nuevos tipos de datos se exponen en un modo compatible con ADO. Además, el controlador OLE DB para SQL Server también define una nueva palabra clave de conexión denominada **DataTypeCompatibility** que se establece en la cadena de conexión.  

> [!NOTE]  
>  Las aplicaciones ADO existentes pueden obtener acceso y actualizar XML, UDT, texto de valores grandes y valores de campo binarios mediante el proveedor SQLOLEDB. El nuevo mayor **varchar (max)**, **nvarchar (max)**, y **varbinary (max)** tipos de datos se devuelven como los tipos ADO **adLongVarChar**, **adLongVarWChar** y **adLongVarBinary** respectivamente. Las columnas XML se devuelven como **adLongVarChar**, y las columnas UDT se devuelven como **adVarBinary**. Sin embargo, si utiliza el controlador OLE DB para SQL Server (MSOLEDBSQL) en lugar de SQLOLEDB, debe asegurarse de establecer la **DataTypeCompatibility** palabra clave en "80" para que los nuevos tipos de datos se asignen correctamente a los tipos de datos de ADO.  

## <a name="enabling-ole-db-driver-for-sql-server-from-ado"></a>Habilitar el controlador OLE DB para SQL Server desde ADO  
 Para habilitar el uso del controlador de OLE DB para SQL Server, las aplicaciones ADO necesita implementar las siguientes palabras clave en sus cadenas de conexión:  

-   `Provider=MSOLEDBSQL`  

-   `DataTypeCompatibility=80`  

 Para obtener más información acerca de la propiedad ADO cadenas de conexión de palabras clave que se admiten en el controlador de OLE DB para SQL Server, vea [Using Connection String Keywords con controlador OLE DB para SQL Server](../../oledb/applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md).  

 El siguiente es un ejemplo de establecimiento de una cadena de conexión de ADO totalmente habilitada para trabajar con el controlador OLE DB para SQL Server, incluida la habilitación de la característica MARS:  

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
 En este ejemplo, un conjunto de registros se utiliza para recuperar y mostrar los datos de una columna XML en el [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **AdventureWorks** base de datos de ejemplo.  

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
 En este ejemplo, se construye la cadena de conexión para habilitar MARS a través del controlador de OLE DB para SQL Server y, a continuación, se crean dos objetos de conjunto de registros para ejecutarlos utilizando la misma conexión.  

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

 En versiones anteriores del proveedor OLE DB, este código hacía que se crease una conexión implícita en la segunda ejecución porque solo podía abrirse un conjunto de resultados activo por cada conexión única. Dado que la conexión implícita no estaba agrupada en el grupo de conexiones OLE DB, esto produciría una sobrecarga adicional. Con la característica MARS expuesta por el controlador OLE DB para SQL Server, se obtienen varios resultados activos en una conexión.  

## <a name="see-also"></a>Vea también  
 [Generar aplicaciones con el controlador OLE DB para SQL Server](../../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)  
