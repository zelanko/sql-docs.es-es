---
title: Errores de proveedor | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- errors collection [ADO]
- provider errors [ADO]
- event-related errors [ADO]
- errors [ADO], provider
- Error object [ADO], provider errors
ms.assetid: cc7d6ff9-2034-45c6-9d61-90b177010054
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 56fff67f882eceec3c07553e5c465da65a69ce65
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66718680"
---
# <a name="provider-errors"></a>Errores del proveedor
Cuando se produce un error de proveedor, se devuelve un error de tiempo de ejecución de -2147467259. Cuando reciba este error, compruebe el **errores** colección de activo **conexión** objeto, que contiene uno o varios errores que describe lo que ha sucedido.  
  
## <a name="the-ado-errors-collection"></a>La colección de errores de ADO  
 Dado que una operación de ADO determinada puede producir varios errores de proveedor, ADO expone una colección de objetos de error a través de la **conexión** objeto. Esta colección no contiene ningún objeto si una operación concluye correctamente y contiene uno o varios **Error** objetos si algo ha ido mal y el proveedor genera uno o varios errores. Examine cada objeto de error para determinar la causa exacta del error.  
  
 Tan pronto como haya terminado de controlar los errores que se han producido, puede borrar la colección mediante una llamada a la **borrar** método. Es especialmente importante borrar explícitamente la **errores** colección antes de llamar a la **Resync**, **UpdateBatch**, o **CancelBatch**método en un **Recordset** objeto, el **abierto** método en un **conexión** de objeto, o establecer el **filtro** propiedad en un **Recordset** objeto. Borra la colección explícitamente, puede estar seguro de que cualquier **Error** en la colección no quedan objetos de una operación anterior.  
  
 Algunas operaciones pueden generar advertencias además de errores. Las advertencias también se representan mediante **Error** objetos en el **errores** colección. Cuando un proveedor agrega una advertencia a la colección, no genera un error en tiempo de ejecución. Compruebe el **recuento** propiedad de la **errores** colección para determinar si una advertencia fue generada por una operación determinada. Si el recuento es uno o más, un **Error** objeto se ha agregado a la colección. Tan pronto como haya determinado que el **errores** colección contiene errores o advertencias, puede recorrer en iteración la colección y recuperar información sobre cada **Error** objeto que contiene. El siguiente ejemplo de Visual Basic corto muestra esto:  
  
```  
' BeginErrorHandlingVB02  
Private Function DeleteCustomer(ByVal CompanyName As String) As Long  
    On Error GoTo DeleteCustomerError  
  
    rst.Find "CompanyName='" & CompanyName & "'"  
DeleteCustomerError:  
Dim objError As ADODB.Error  
Dim strError As String  
  
    If cnn.Errors.Count > 0 Then  
        For Each objError In cnn.Errors  
            strError = strError & "Error #" & objError.Number & _  
                " " & objError.Description & vbCrLf & _  
                "NativeError: " & objError.NativeError & vbCrLf & _  
                "SQLState: " & objError.SQLState & vbCrLf & _  
                "Reported by: " & objError.Source & vbCrLf & _  
                "Help file: " & objError.HelpFile & vbCrLf & _  
                "Help Context ID: " & objError.HelpContext  
        Next  
        MsgBox strError  
    End If  
End Function  
' EndErrorHandlingVB02  
```  
  
 La rutina de control de errores incluye un **para cada** bucle que examina cada objeto de la **errores** colección. En este ejemplo, acumula un mensaje para su presentación. En un programa, debe escribir código para realizar una tarea adecuada para cada error, como cerrar todos los archivos de abrir y va a cerrar el programa de manera ordenada.  
  
## <a name="the-error-object"></a>El objeto de Error  
 Examinando un **Error** objeto puede determinar cuál fue el error, y más importante, qué aplicación o el objeto que produjo el error. El **Error** objeto tiene las siguientes propiedades:  
  
|Nombre de propiedad|Descripción|  
|-------------------|-----------------|  
|**Descripción**|Descripción de texto del error que se ha producido.|  
|**HelpContext, HelpFile**|Hace referencia al archivo de ayuda y el tema de ayuda que contiene una descripción del error que se ha producido.|  
|**NativeError**|El número de error específico del proveedor.|  
|**Número**|Un entero largo que representa el número (enumerados en el **ErrorValueEnum**) del error que se ha producido.|  
|**Source**|Indica el nombre del objeto o aplicación que generó un error.|  
|**SQLState**|Un código de error de cinco caracteres que devuelve el proveedor durante el proceso de una instrucción SQL.|  
  
 ADO **Error** objeto es muy similar a la versión estándar de Visual Basic **Err** objeto. Sus propiedades describen el error producido. Además del número del error, también recibirá dos fragmentos de información relacionados. El **NativeError** propiedad contiene un número de error específico del proveedor que está usando. En el ejemplo anterior, el proveedor es el proveedor Microsoft OLE DB para SQL Server, por lo que **NativeError** contendrá errores específicos de SQL Server. El **SQLState** propiedad tiene un código de cinco letras que describe un error en una instrucción SQL.  
  
## <a name="event-related-errors"></a>Errores relacionados con eventos  
 El **Error** objeto también se utiliza cuando se producen errores relacionados con eventos. Puede determinar si se produjo un error en el proceso que se genera un evento de ADO activando el **Error** objeto pasado como un parámetro de evento.  
  
 Si la operación que provoca un evento concluye correctamente, el *adStatus* parámetro del controlador de eventos se establecerá en *adStatusOK*. Por otro lado, si la operación que provocó el evento se realizó correctamente, el *adStatus* parámetro está establecido en *adStatusErrorsOccurred*. En ese caso, el *pError* parámetro contendrá un **Error** objeto que describe el error.
