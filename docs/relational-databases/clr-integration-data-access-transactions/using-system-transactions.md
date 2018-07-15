---
title: Utilizar System.Transactions | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: clr
ms.tgt_pltfrm: ''
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- TransactionScope class
- Dispose method
- System.Transactions namespace
ms.assetid: 79656ce5-ce46-4c5e-9540-cf9869bd774b
caps.latest.revision: 16
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: e9e09ae1d55065f7f50d25c3538f3c9218d8ed52
ms.sourcegitcommit: 022d67cfbc4fdadaa65b499aa7a6a8a942bc502d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/03/2018
ms.locfileid: "37349812"
---
# <a name="using-systemtransactions"></a>Utilizar System.Transactions
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  El espacio de nombres **System.Transactions** proporciona un nuevo marco de transacciones totalmente integrado con ADO.NET y la característica de integración con Common Language Runtime (CLR) en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . La clase **System.Transactions.TransactionScope** crea un bloque de código transaccional dando de alta implícitamente las conexiones en una transacción distribuida. Se debe llamar al método **Complete** al final del bloque de código marcado por **TransactionScope**. Se llama al método **Dispose** cuando la ejecución de programas deja un bloque de código, lo que hace que se interrumpa la transacción si no se llama al método **Complete** . Si se ha producido una excepción que hace que el código deje el ámbito, se considera que la transacción se ha interrumpido.  
  
 Se recomienda emplear un bloque **using** para asegurarse de que se llama al método **Dispose** en el objeto **TransactionScope** cuando se sale del bloque **using** . El hecho de no confirmar o revertir las transacciones pendientes puede reducir significativamente el rendimiento, porque el tiempo de espera predeterminado para **TransactionScope** es un minuto. Si no utiliza una instrucción **using** , debe realizar todo el trabajo de un bloque **Try** y llamar explícitamente al método **Dispose** del bloque **Finally** .  
  
 Si se produce una excepción dentro de **TransactionScope**, la transacción se marca como incoherente y se abandona. Se revierte cuando se elimina **TransactionScope** . Si no se produce ninguna excepción, las transacciones participantes se confirman.  
  
 Se debe utilizar**TransactionScope** solamente cuando se tiene acceso a orígenes de datos locales y remotos o a administradores de recursos externos. Esto se debe a que **TransactionScope** siempre hace que se promuevan las transacciones, aunque solo se esté utilizando dentro de una conexión de contexto.  
  
> [!NOTE]  
>  La clase **TransactionScope** crea una transacción con **System.Transactions.Transaction.IsolationLevel** de **Serializable** de forma predeterminada. Dependiendo de la aplicación, puede considerar la opción de reducir el nivel de aislamiento para evitar conflictos en ella.  
  
> [!NOTE]  
>  Se recomienda realizar solo actualizaciones, inserciones, y eliminaciones dentro de las transacciones distribuidas en servidores remotos porque consumen una gran cantidad de recursos de la base de datos. Si la operación se va a realizar en el servidor local, no hace falta una transacción distribuida y bastará con una transacción local. Las instrucciones SELECT pueden bloquear innecesariamente los recursos de la base de datos y, en algunas situaciones, puede que sea necesario utilizar transacciones para las mismas. Cualquier trabajo no relacionado con la base de datos se debe llevar a cabo fuera del ámbito de la transacción, a menos que implique a otros administradores de recursos con transacciones. Aunque una excepción dentro del ámbito de la transacción impide que se confirme la transacción, la clase **TransactionScope** no tiene medios para revertir los cambios que haya realizado el código fuera del ámbito de la propia transacción. Si tiene que realizar alguna acción cuando se revierte la transacción, debe escribir su propia implementación de la interfaz **System.Transactions.IEnlistmentNotification** y dar de alta explícitamente la transacción.  
  
## <a name="example"></a>Ejemplo  
 Para trabajar con **System.Transactions**, debe tener una referencia al archivo System.Transactions.dll.  
  
 El código siguiente muestra cómo crear una transacción que se puede promover en dos instancias diferentes de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Estas instancias están representadas por dos objetos **System.Data.SqlClient.SqlConnection** diferentes, que se incluyen en un bloque **TransactionScope** . El código crea el bloque **TransactionScope** con una instrucción **using** y abre la primera conexión, que automáticamente lo da de alta en **TransactionScope**. La transacción se da de alta inicialmente como una transacción ligera, no como una transacción distribuida completa. El código supone la existencia de lógica condicional (que se ha omitido por razones de brevedad). Solo abre la segunda conexión si es necesario, dándola de alta en **TransactionScope**. Cuando se abre la conexión, la transacción se promueve automáticamente a una transacción distribuida completa. El código llama entonces a **TransactionScope.Complete**, que confirma la transacción. El código elimina las dos conexiones al salir de las instrucciones **using** para las conexiones. Se llama automáticamente al método **TransactionScope.Dispose** para **TransactionScope** a la terminación del bloque **using** para **TransactionScope**. Si se ha producido una excepción en algún punto del bloque **TransactionScope** , no se llama a **Complete** y la transacción distribuida se revertirá cuando se elimine **TransactionScope** .  
  
 Visual Basic  
  
```  
Using transScope As New TransactionScope()  
    Using connection1 As New SqlConnection(connectString1)  
        ' Opening connection1 automatically enlists it in the   
        ' TransactionScope as a lightweight transaction.  
        connection1.Open()  
  
        ' Do work in the first connection.  
  
        ' Assumes conditional logic in place where the second  
        ' connection will only be opened as needed.  
        Using connection2 As New SqlConnection(connectString2)  
            ' Open the second connection, which enlists the   
            ' second connection and promotes the transaction to  
            ' a full distributed transaction.  
            connection2.Open()  
  
            ' Do work in the second connection.  
  
        End Using  
    End Using  
  
    ' Commit the transaction.  
    transScope.Complete()  
End Using  
```  
  
 C#  
  
```  
using (TransactionScope transScope = new TransactionScope())  
{  
    using (SqlConnection connection1 = new   
       SqlConnection(connectString1))  
    {  
        // Opening connection1 automatically enlists it in the   
        // TransactionScope as a lightweight transaction.  
        connection1.Open();  
  
        // Do work in the first connection.  
  
        // Assumes conditional logic in place where the second  
        // connection will only be opened as needed.  
        using (SqlConnection connection2 = new   
            SqlConnection(connectString2))  
        {  
            // Open the second connection, which enlists the   
            // second connection and promotes the transaction to  
            // a full distributed transaction.   
            connection2.Open();  
  
            // Do work in the second connection.  
        }  
    }  
    //  The Complete method commits the transaction.  
    transScope.Complete();  
}  
```  
  
## <a name="see-also"></a>Vea también  
 [Integración CLR y transacciones](../../relational-databases/clr-integration-data-access-transactions/clr-integration-and-transactions.md)  
  
  
