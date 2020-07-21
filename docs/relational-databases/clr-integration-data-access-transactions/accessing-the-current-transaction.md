---
title: Obtener acceso a la transacción actual | Microsoft Docs
description: En SQL Server integración CLR, la propiedad actual de la clase System. Transactions. Transaction permite tener acceso a la transacción actual.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- current transaction access
- Current property
- Transaction class
ms.assetid: 1a4e2ce5-f627-4c81-8960-6a9968cefda2
author: rothja
ms.author: jroth
ms.openlocfilehash: c82c4e4f5b1f1af6194ff409a684ca239881487a
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85765402"
---
# <a name="accessing-the-current-transaction"></a>Obtener acceso a la transacción actual
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Si una transacción se encuentra activa en el momento en que se escribe el código de Common Language Runtime (CLR) que se ejecuta en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , la transacción se expone a través de la clase **System.Transactions.Transaction** . La propiedad **Transaction.Current** permite obtener acceso a la transacción actual. En la mayoría de los casos, no es necesario obtener acceso a la transacción de forma explícita. Para las conexiones de bases de datos, ADO.NET comprueba **Transaction.Current** de forma automática cuando se llama al método **Connection.Open** y da de alta la conexión en esa transacción de forma transparente (a menos que la palabra clave **Enlist** esté establecida en False en la cadena de conexión).  
  
 Es posible que desee usar directamente el objeto **Transaction** en los escenarios siguientes:  
  
-   Si desea dar de alta un recurso que no se da de alta de manera automática o que, por alguna razón, no se haya dado de alta durante la inicialización.  
  
-   Si desea dar de alta un recurso de forma explícita en la transacción.  
  
-   Si desea finalizar la transacción externa desde el interior de su función o procedimiento almacenado. En este caso, use <xref:System.Transactions.TransactionScope>. Por ejemplo, el código siguiente revertirá la transacción actual:  
  
    ```  
    using(TransactionScope transactionScope = new TransactionScope(TransactionScopeOptions.Required)) { }  
    ```  
  
 En el resto de este tema se describen otras formas de cancelar una transacción externa.  
  
## <a name="canceling-an-external-transaction"></a>Cancelar una transacción externa  
 Puede cancelar las transacciones externas de una función o de un procedimiento administrado de las siguientes formas:  
  
-   La función o el procedimiento administrado puede devolver un valor utilizando un parámetro de salida. El procedimiento [!INCLUDE[tsql](../../includes/tsql-md.md)] de llamada puede comprobar el valor devuelto y, si procede, ejecutar **ROLLBACK TRANSACTION**.  
  
-   La función o el procedimiento administrado puede iniciar una excepción personalizada. El procedimiento [!INCLUDE[tsql](../../includes/tsql-md.md)] de llamada puede detectar la excepción iniciada por la función o por el procedimiento administrado en un bloque try/catch y ejecutar **ROLLBACK TRANSACTION**.  
  
-   La función o el procedimiento administrado puede cancelar la transacción actual llamando al método **Transaction.Rollback** si se cumple una condición determinada.  
  
 Cuando se llama al método **Transaction.Rollback** dentro de una función o de un procedimiento administrado, éste inicia una excepción con un mensaje de error ambiguo y puede colocarse dentro de un bloque try/catch. El mensaje de error puede ser similar al siguiente:  
  
```  
Msg 3994, Level 16, State 1, Procedure uspRollbackFromProc, Line 0  
Transaction is not allowed to roll back inside a user defined routine, trigger or aggregate because the transaction is not started in that CLR level. Change application logic to enforce strict transaction nesting.  
```  
  
 Se espera esta excepción y el bloque try/catch resulta necesario para que continúe la ejecución del código. Sin el bloque try/catch, la excepción se iniciará inmediatamente en el procedimiento [!INCLUDE[tsql](../../includes/tsql-md.md)] de llamada y finalizará la ejecución del código administrado. Cuando finaliza la ejecución del código administrado, se inicia otra excepción:  
  
```  
Msg 3991, Level 16, State 1, Procedure uspRollbackFromProc, Line 1   
The context transaction which was active before entering user defined routine, trigger or aggregate " uspRollbackFromProc " has been ended inside of it, which is not allowed. Change application logic to enforce strict transaction nesting. The statement has been terminated.  
```  
  
 También se espera esta excepción y, para continuar, debe incluir un bloque try/catch alrededor de la instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)] que realiza la acción que activa el desencadenador. A pesar de las dos excepciones iniciadas, la transacción se revierte y no se confirman los cambios.  
  
### <a name="example"></a>Ejemplo  
 A continuación se muestra un ejemplo de una transacción que se revierte desde un procedimiento administrado mediante el uso del método **Transaction.Rollback** . Observe el bloque try/catch alrededor del método **Transaction.Rollback** en el código administrado. El script [!INCLUDE[tsql](../../includes/tsql-md.md)] crea un ensamblado y un procedimiento almacenado administrado. Tenga en cuenta que la instrucción **EXEC uspRollbackFromProc** se incluye en un bloque try/catch, de modo que la excepción iniciada se detecta al completarse la ejecución del procedimiento administrado.  
  
```csharp  
using System;  
using System.Data;  
using System.Data.SqlClient;  
using System.Data.SqlTypes;  
using Microsoft.SqlServer.Server;  
using System.Transactions;  
  
public partial class StoredProcedures  
{  
[Microsoft.SqlServer.Server.SqlProcedure]  
public static void uspRollbackFromProc()  
{  
   using (SqlConnection connection = new SqlConnection(@"context connection=true"))  
   {  
      // Open the connection.  
      connection.Open();  
  
      bool successCondition = true;  
  
      // Success condition is met.  
      if (successCondition)  
      {  
         SqlContext.Pipe.Send("Success condition met in procedure.");   
         // Perform other actions here.  
      }  
  
      //  Success condition is not met, the transaction will be rolled back.  
      else  
      {  
         SqlContext.Pipe.Send("Success condition not met in managed procedure. Transaction rolling back...");  
         try  
         {  
               // Get the current transaction and roll it back.  
               Transaction trans = Transaction.Current;  
               trans.Rollback();  
         }  
         catch (SqlException ex)  
         {  
            // Catch the expected exception.   
            // This allows the connection to close correctly.                      
         }    
      }  
  
      // Close the connection.  
      connection.Close();  
   }  
}  
};  
```  
  
```vb  
Imports System  
Imports System.Data  
Imports System.Data.SqlClient  
Imports System.Data.SqlTypes  
Imports Microsoft.SqlServer.Server  
Imports System.Transactions  
  
Partial Public Class StoredProcedures  
<Microsoft.SqlServer.Server.SqlProcedure()> _  
Public Shared Sub  uspRollbackFromProc ()  
   Using connection As New SqlConnection("context connection=true")  
  
   ' Open the connection.  
   connection.Open()  
  
   Dim successCondition As Boolean  
   successCondition = False  
  
   ' Success condition is met.  
   If successCondition Then  
  
      SqlContext.Pipe.Send("Success condition met in procedure.")  
  
      ' Success condition is not met, the transaction will be rolled back.  
  
   Else  
      SqlContext.Pipe.Send("Success condition not met in managed procedure. Transaction rolling back...")  
      Try  
         ' Get the current transaction and roll it back.  
         Dim trans As Transaction  
         trans = Transaction.Current  
         trans.Rollback()  
  
      Catch ex As SqlException  
         ' Catch the exception instead of throwing it.    
         ' This allows the connection to close correctly.                      
      End Try  
  
   End If  
  
   ' Close the connection.  
   connection.Close()  
  
End Using  
End Sub  
End Class  
```  
  
 **Transact-SQL**  
  
```  
--Register assembly.  
CREATE ASSEMBLY TestProcs FROM 'C:\Programming\TestProcs.dll'   
Go  
CREATE PROCEDURE uspRollbackFromProc AS EXTERNAL NAME TestProcs.StoredProcedures.uspRollbackFromProc  
Go  
  
-- Execute procedure.  
BEGIN TRY  
BEGIN TRANSACTION   
-- Perform other actions.  
Exec uspRollbackFromProc  
-- Perform other actions.  
PRINT N'Commiting transaction...'  
COMMIT TRANSACTION  
END TRY  
  
BEGIN CATCH  
SELECT ERROR_NUMBER() AS ErrorNum, ERROR_MESSAGE() AS ErrorMessage  
PRINT N'Exception thrown, rolling back transaction.'  
ROLLBACK TRANSACTION  
PRINT N'Transaction rolled back.'   
END CATCH  
Go  
  
-- Clean up.  
DROP Procedure uspRollbackFromProc;  
Go  
DROP ASSEMBLY TestProcs;  
Go  
```  
  
## <a name="see-also"></a>Consulte también  
 [Integración CLR y transacciones](../../relational-databases/clr-integration-data-access-transactions/clr-integration-and-transactions.md)  
  
  
