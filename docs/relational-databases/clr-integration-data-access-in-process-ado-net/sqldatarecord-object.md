---
title: Objeto SqlDataRecord | Microsoft Docs
description: En la integración de CLR de SQL Server, los procedimientos almacenados pueden utilizar la clase SqlDataRecord para enviar conjuntos de resultados personalizados al cliente.
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- SqlDataRecord object
- custom result sets [CLR integration]
ms.assetid: 2ed667fb-749c-4280-a8fb-650643683c8f
author: rothja
ms.author: jroth
ms.openlocfilehash: 4aa5ea4d06ac5b8da69eec246387007ba5d03606
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81487515"
---
# <a name="sqldatarecord-object"></a>SqlDataRecord, objeto
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  El objeto **SqlDataRecord** representa una fila única de datos, junto con sus metadatos relacionados.  
  
 Los procedimientos almacenados administrados se pueden enviar a los conjuntos de resultados del cliente que no son de **SqlDataReader**. La clase **SqlDataRecord** , junto con los métodos **SendResultsStart**, **SendResultsRow**y **SendResultsEnd** del objeto **SqlPipe** , permite a los procedimientos almacenados enviar conjuntos de resultados personalizados al cliente.  
  
 Para obtener más información, vea la documentación de referencia de la clase **Microsoft.SqlServer.Server.SqlDataRecord** en la documentación del SDK de .NET Framework.  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente se crea un nuevo registro de empleado y se devuelve al autor de la llamada.  
  
 C#  
  
```  
[Microsoft.SqlServer.Server.SqlProcedure]  
public static void CreateNewRecordProc()  
{  
    // Variables.         
    SqlDataRecord record;  
  
    // Create a new record with the column metadata.  The constructor   
    // is able to accept a variable number of parameters.  
    record = new SqlDataRecord(new SqlMetaData("EmployeeID", SqlDbType.Int),  
                               new SqlMetaData("Surname", SqlDbType.NVarChar, 20),  
                               new SqlMetaData("GivenName", SqlDbType.NVarChar, 20),  
                               new SqlMetaData("StartDate", SqlDbType.DateTime) );  
  
    // Set the record fields.  
    record.SetInt32(0, 0042);  
    record.SetString(1, "Funk");  
    record.SetString(2, "Don");  
    record.SetDateTime(3, new DateTime(2005, 7, 17));  
  
    // Send the record to the calling program.  
    SqlContext.Pipe.Send(record);  
  
}  
```  
  
 Visual Basic  
  
```  
<Microsoft.SqlServer.Server.SqlProcedure()> _  
Public Shared Sub  CreateNewRecordVBProc ()  
    ' Variables.  
    Dim record As SqlDataRecord  
  
    ' Create a new record with the column metadata. The constructor is   
    ' able to accept a variable number of parameters  
  
    record = New SqlDataRecord(New SqlMetaData("EmployeeID", SqlDbType.Int), _  
                           New SqlMetaData("Surname", SqlDbType.NVarChar, 20), _  
                           New SqlMetaData("GivenName", SqlDbType.NVarChar, 20), _  
                           New SqlMetaData("StartDate", SqlDbType.DateTime))  
  
    ' Set the record fields.  
    record.SetInt32(0, 42)  
    record.SetString(1, "Funk")  
    record.SetString(2, "Don")  
    record.SetDateTime(3, New DateTime(2005, 7, 17))  
  
    ' Send the record to the calling program.  
    SqlContext.Pipe.Send(record)  
  
End Sub  
```  
  
## <a name="see-also"></a>Consulte también  
 [SqlPipe, objetos](../../relational-databases/clr-integration-data-access-in-process-ado-net/sqlpipe-object.md)  
  
  
