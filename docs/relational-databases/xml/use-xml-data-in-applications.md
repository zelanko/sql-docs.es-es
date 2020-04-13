---
title: Usar datos XML en las aplicaciones | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- parameters [XML in SQL Server]
- XML [SQL Server], ADO
- columns [XML in SQL Server], ADO.NET
- ADO [XML in SQL Server]
- columns [XML in SQL Server], SQL Server Native Client
- xml data type [SQL Server], ADO
- SQLNCLI, XML
- xml data type [SQL Server], SQL Server Native Client
- SQL Server Native Client, XML
- ADO.NET [XML in SQL Server]
- XML [SQL Server], ADO.NET
- columns [XML in SQL Server], ADO
- xml data type [SQL Server], ADO.NET
- XML [SQL Server], SQL Server Native Client
ms.assetid: 5dabf7e0-c6df-451d-a070-4661f84607fd
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fa573c4d824d8a1f419335fa0c7b3d451b80f96e
ms.sourcegitcommit: 68583d986ff5539fed73eacb7b2586a71c37b1fa
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/04/2020
ms.locfileid: "80664986"
---
# <a name="use-xml-data-in-applications"></a>Usar datos XML en las aplicaciones
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  En este tema se describen las opciones que están disponibles para trabajar con tipos de datos **xml** en una aplicación. El tema incluye información acerca de lo siguiente:  
  
-   Controlar XML desde una columna de tipo **xml** usando ADO y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client  
  
-   Controlar XML desde una columna de tipo **xml** utilizando ADO.NET  
  
-   Controlar el tipo **xml** en parámetros utilizando ADO.NET  
  
## <a name="handling-xml-from-an-xml-type-column-by-using-ado-and-sql-server-native-client"></a>Controlar XML desde una columna de tipo XML usando ADO y SQL Server Native Client  
 Para usar componentes MDAC con el fin de obtener acceso a los tipos y características introducidos en [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], debe establecer la propiedad de inicialización DataTypeCompatibility en la cadena de conexión de ADO.  
  
 Por ejemplo, en el siguiente ejemplo de Visual Basic Scripting Edition (VBScript) se muestra el resultado de la realización de una consulta a una columna de tipo de datos **xml** , `Demographics`, de la tabla `Sales.Store` de la base de datos de ejemplo `AdventureWorks2012` . Específicamente, la consulta busca el valor de la instancia de esta columna para la fila en la que `CustomerID` es igual a `3`.  
  
```  
Const DS = "MyServer"  
Const DB = "AdventureWorks2012"  
  
Set objConn = CreateObject("ADODB.Connection")  
Set objRs = CreateObject("ADODB.Recordset")  
  
CommandText = "SELECT Demographics" & _  
              " FROM Sales.Store" & _  
              " INNER JOIN Sales.Customer" & _  
              " ON Sales.Store.BusinessEntityID = sales.customer.StoreID" & _  
              " WHERE Sales.Customer.CustomerID = 3" & _  
              " OR Sales.Customer.CustomerID = 4"  
  
ConnectionString = "Provider=SQLNCLI11" & _  
                   ";Data Source=" & DS & _  
                   ";Initial Catalog=" & DB & _  
                   ";Integrated Security=SSPI;" & _  
                   "DataTypeCompatibility=80"  
  
'Connect to the data source.  
objConn.Open ConnectionString  
  
'Execute command through the connection and display  
Set objRs = objConn.Execute(CommandText)  
  
Dim rowcount  
rowcount = 0  
Do While Not objRs.EOF  
   rowcount = rowcount + 1  
   MsgBox "Row " & rowcount & _  
           vbCrLf & vbCrLf & objRs(0)  
   objRs.MoveNext  
Loop  
  
'Clean up.  
objRs.Close  
objConn.Close  
Set objRs = Nothing  
Set objConn = Nothing  
```  
  
 Este ejemplo muestra cómo establecer la propiedad de compatibilidad de tipos de datos. De manera predeterminada, se establece en 0 cuando se usa [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client. Si establece el valor en 80, el proveedor de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client hará que las columnas de tipo **xml** y las definidas por el usuario aparezcan como tipos de datos de [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] . Serán DBTYPE_WSTR y DBTYPE_BYTES, respectivamente.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client también debe estar instalado en el equipo cliente y la cadena de conexión debe especificar que se use como proveedor de datos con "`Provider=SQLNCLI11;...`".  
  
#### <a name="to-test-this-example"></a>Para probar este ejemplo  
  
1.  Compruebe que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client está instalado y que en el equipo cliente está disponible MDAC 2.6 o versiones posteriores.  
  
     Para obtener más información, consulte [Programación de SQL Server Native Client](../../relational-databases/native-client/sql-server-native-client-programming.md).  
  
2.  Compruebe que la base de datos de ejemplo [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está instalada.  
  
     Este ejemplo requiere la base de datos de ejemplo [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] .  
  
3.  Copie el código que se mostró anteriormente en este tema y péguelo en su editor de texto o de código. Guarde el archivo como HandlingXmlDataType.vbs.  
  
4.  Modifique el script según sea necesario por la instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y guarde los cambios.  
  
     Por ejemplo, donde se especifique `MyServer` , debe sustituirlo por `(local)` o por el nombre real del servidor en el que está instalado [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
5.  Ejecute HandlingXmlDataType.vbs y ejecute el script.  
  
 Los resultados serán similares a los de la siguiente salida de ejemplo:  
  
```  
Row 1  
  
<StoreSurvey xmlns="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/StoreSurvey">  
  <AnnualSales>1500000</AnnualSales>  
  <AnnualRevenue>150000</AnnualRevenue>  
  <BankName>Primary International</BankName>  
  <BusinessType>OS</BusinessType>  
  <YearOpened>1974</YearOpened>  
  <Specialty>Road</Specialty>  
  <SquareFeet>38000</SquareFeet>  
  <Brands>3</Brands>  
  <Internet>DSL</Internet>  
  <NumberEmployees>40</NumberEmployees>  
</StoreSurvey>  
  
Row 2  
  
<StoreSurvey xmlns="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/StoreSurvey">  
  <AnnualSales>300000</AnnualSales>  
  <AnnualRevenue>30000</AnnualRevenue>  
  <BankName>United Security</BankName>  
  <BusinessType>BM</BusinessType>  
  <YearOpened>1976</YearOpened>  
  <Specialty>Road</Specialty>  
  <SquareFeet>6000</SquareFeet>  
  <Brands>2</Brands>  
  <Internet>DSL</Internet>  
  <NumberEmployees>5</NumberEmployees>  
</StoreSurvey>  
```  
  
## <a name="handling-xml-from-an-xml-type-column-by-using-adonet"></a>Controlar XML desde una columna de tipo xml utilizando ADO.NET  
 Para controlar XML desde una columna de tipo de datos **xml** mediante ADO.NET y [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)], puede usar el comportamiento estándar de la clase **SqlCommand**. Por ejemplo, una columna de tipo de datos **xml** y sus valores se pueden recuperar de la misma manera que se recupera cualquier columna SQL utilizando una clase **SqlDataReader**. Sin embargo, si desea trabajar con el contenido de una columna de tipo de datos **xml** como XML, primero tendrá que asignar el contenido a un tipo **XmlReader** .  
  
 Para obtener más información y código de ejemplo, vea el artículo sobre valores de columnas XML en un lector de datos de la documentación del SDK de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnlong](../../includes/dnprdnlong-md.md)].  
  
## <a name="handling-an-xml-type-column-in-parameters-by-using-adonet"></a>Controlar una columna de tipo XML como parámetros mediante ADO.NET  
 Para controlar un tipo de datos XML pasado como un parámetro en ADO.NET y [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)], puede indicar el valor como una instancia del tipo de datos **SqlXml** . No es necesario llevar a cabo ningún control especial, porque las columnas de tipo de datos **xml** de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pueden aceptar valores de parámetros del mismo modo que otros tipos de columnas y de datos, como **string** o **integer**.  
  
 Para obtener más información y código de ejemplo, vea el artículo sobre valores XML como parámetros de comando de la documentación del SDK de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnlong](../../includes/dnprdnlong-md.md)].  
  
## <a name="see-also"></a>Consulte también  
 [Datos XML &#40;SQL Server&#41;](../../relational-databases/xml/xml-data-sql-server.md)  
  
  
