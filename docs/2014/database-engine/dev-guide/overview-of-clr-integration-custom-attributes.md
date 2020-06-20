---
title: Información general sobre los atributos personalizados de la integración CLR | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: reference
helpviewer_keywords:
- custom attributes [CLR integration]
- attributes [CLR integration]
- common language runtime [SQL Server], attributes
- database objects [CLR integration], custom attributes
- building database objects [CLR integration], custom attributes
ms.assetid: ecf5c097-0972-48e2-a9c0-b695b7dd2820
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 43db9f034a759e9c041f5cc6ab95baa5af4d7353
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84933466"
---
# <a name="overview-of-clr-integration-custom-attributes"></a>Información general de los atributos personalizados de la integración CLR
  El Common Language Runtime (CLR) de [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] permite el uso de palabras clave descriptivas, llamadas atributos. Estos atributos proporcionan información adicional para muchos elementos, tales como métodos y clases. Los atributos se guardan en el ensamblado con los metadatos del objeto y se pueden utilizar para describir el código a otras herramientas de desarrollo, o para alterar el comportamiento en tiempo de ejecución dentro de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Al registrar una rutina CLR con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deriva un conjunto de propiedades sobre la rutina. Estas propiedades rutinarias determinan las capacidades de la rutina, incluido si se puede indizar la rutina. Por ejemplo, establecer la propiedad `DataAccess` en `DataAccessKind.Read` permite tener acceso a datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dentro de una función CLR. En el ejemplo siguiente se muestra un caso simple en el que la `DataAccess` propiedad se establece para facilitar el acceso a datos desde una tabla de usuario **Table1**.  
  
```csharp  
using System;  
using System.Data;  
using System.Data.Sql;  
using System.Data.SqlTypes;  
using Microsoft.SqlServer.Server;  
using System.Data.SqlClient;  
  
public partial class UserDefinedFunctions  
{  
    [SqlFunction(DataAccess = DataAccessKind.Read)]  
    public static string func1()  
    {  
        // Open a connection and create a command  
        SqlConnection conn = new SqlConnection("context connection = true");  
        conn.Open();  
        SqlCommand cmd = conn.CreateCommand();  
        cmd.CommandText = "SELECT str_val FROM table1 WHERE int_val = 10";  
        // where table1 is a user table  
        // Execute this command   
        SqlDataReader rd = cmd.ExecuteReader();  
        // Set string ret_val to str_val returned from the query  
        string ret_val = rd.GetValue(0).ToString();  
        rd.Close();  
        return ret_val;  
    }  
}  
```  
  
```vb  
Imports System  
Imports System.Data  
Imports System.Data.Sql  
Imports System.Data.SqlTypes  
Imports Microsoft.SqlServer.Server  
Imports System.Data.SqlClient  
  
Public partial Class UserDefinedFunctions  
    <SqlFunction(DataAccess = DataAccessKind.Read)> _   
    Public Shared Function func1() As String  
        ' Open a connection and create a command  
        Dim conn As SqlConnection = New SqlConnection("context connection = true")   
        conn.Open()  
        Dim cmd As SqlCommand =  conn.CreateCommand()   
        cmd.CommandText = "SELECT str_val FROM table1 WHERE int_val = 10"  
        ' where table1 is a user table  
        ' Execute this command   
        Dim rd As SqlDataReader =  cmd.ExecuteReader()   
        ' Set string ret_val to str_val returned from the query  
        Dim ret_val As String =  rd.GetValue(0).ToString()   
        rd.Close()  
        Return ret_val  
    End Function  
End Class  
```  
  
 Para las rutinas [!INCLUDE[tsql](../../includes/tsql-md.md)], [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deriva directamente las propiedades de la rutina de la definición de rutina. Para las rutinas CLR, el servidor no analiza el cuerpo de la rutina para derivar estas propiedades. En su lugar, puede utilizar atributos personalizados para las clases y miembros de clase implementados en un lenguaje [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)].  
  
 Los atributos personalizados necesarios para las rutinas CLR, los tipos definidos por el usuario y los agregados se definen en el espacio de nombres `Microsoft.SqlServer.Server`.  
  
## <a name="see-also"></a>Consulte también  
 [Atributos personalizados para las rutinas CLR](../../relational-databases/clr-integration/database-objects/clr-integration-custom-attributes-for-clr-routines.md)  
  
  
