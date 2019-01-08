---
title: Errores de ADO | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 02/15/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- errors [ADO]
ms.assetid: 9bb84114-a1df-4122-a1b8-ad98dcd85cc3
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c5b2d3f43067750d2fc70a86c6a23bc74dd3bbc4
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/28/2018
ms.locfileid: "52509108"
---
# <a name="ado-run-time-errors"></a>Errores de tiempo de ejecución de ADO
Errores de ADO se notifican al programa como errores de tiempo de ejecución. Puede usar el mecanismo de intercepción de errores de su lenguaje de programación para interceptar y controlarlos. Por ejemplo, en Visual Basic, utilice el **On Error** instrucción. En Visual C++, lo depende del método que se usa para tener acceso a las bibliotecas de ADO. Con #import, utilice un **try-catch** bloque. En caso contrario, deben recuperar explícitamente el objeto de error mediante una llamada a los programadores de C++ **GetErrorInfo**. El siguiente procedimiento sub de Visual Basic muestra cómo interceptar un error de ADO:

```
' BeginErrorHandlingVB01
Private Sub Form_Load()
' Turn on error handling
On Error GoTo FormLoadError

'Open the database and the recordset for processing.
'
Dim strCnn As String
strCnn = "Provider=sqloledb;" & _
    "Data Source=a-iresmi2000;" & _
    "Initial Catalog=Northwind;Integrated Security=SSPI"

' cnn is a Public Connection Object because
' it was defined WithEvents
Set cnn = New ADODB.Connection
cnn.Open strCnn

' The next line of code intentionally causes
' an error by trying to open a connection
' that has already been opened.
cnn.Open strCnn

' rst is a Public Recordset because it
' was defined WithEvents
Set rst = New ADODB.Recordset
rst.Open "Customers", cnn

Exit Sub

' Error handler
FormLoadError:
    Dim strErr As String
    Select Case Err
        Case adErrObjectOpen
            strErr = "Error #" & Err.Number & ": " & Err.Description & vbCrLf
            strErr = strErr & "Error reported by: " & Err.Source & vbCrLf
            strErr = strErr & "Help File: " & Err.HelpFile & vbCrLf
            strErr = strErr & "Topic ID: " & Err.HelpContext
            MsgBox strErr
            Debug.Print strErr
            Err.Clear
            Resume Next
        ' If some other error occurs that
        ' has nothing to do with ADO, show
        ' the number and description and exit.
        Case Else
            strErr = "Error #" & Err.Number & ": " & Err.Description & vbCrLf
            MsgBox strErr
            Debug.Print strErr
            Unload Me
    End Select
End Sub
' EndErrorHandlingVB01
```

 Esto **Form_Load** procedimiento de evento intencionadamente crea un error al intentar abrir el mismo **conexión** objeto dos veces. La segunda vez el **abierto** se llama al método, se activa el controlador de errores. En este caso, el error es de tipo **adErrObjectOpen**, por lo que el controlador de errores muestra el siguiente mensaje antes de reanudar la ejecución del programa:

```
Error #3705: Operation is not allowed when the object is open.
Error reported by: ADODB.Connection
Help File: E:\WINNT\HELP\ADO260.CHM Topic ID: 1003705
```

 El mensaje de error incluye cada parte de la información proporcionada por Visual Basic **Err** objeto, excepto el **LastDLLError** valor, que no se aplica aquí. El número de error indica qué error se ha producido. La descripción es útil en casos en los que no desea controlar el error por sí mismo. Puede pasar simplemente lo al usuario. Aunque normalmente es conveniente utilizar mensajes personalizados para su aplicación, no se puede prever cada error; la descripción proporciona algunas pistas sobre qué salió mal. En el código de ejemplo, se notificó el error por el **conexión** objeto. Verá el objeto tipo o identificador de programación: no un nombre de variable.

> [!NOTE]
>  Visual Basic **Err** objeto sólo contiene información sobre el error más reciente. ADO **errores** colección de la **conexión** objeto contiene uno **Error** objeto por cada error generado por la operación más reciente de ADO. Use la **errores** colección en lugar de **Err** objeto para controlar varios errores. Para obtener más información sobre la **errores** colección, consulte [errores del proveedor](../../../ado/guide/data/provider-errors.md). Sin embargo, si no es válido no **conexión** objeto, el **Err** objeto es el único origen para obtener información acerca de los errores de ADO.

 ¿Qué tipos de operaciones pueden provocar errores de ADO? Errores comunes de ADO pueden implicar la apertura de un objeto, como un **conexión** o **Recordset**, intentar actualizar los datos o una llamada a un método o propiedad que no es compatible con su proveedor.

 Errores de OLE DB también se pueden pasar a la aplicación como errores de tiempo de ejecución en el **errores** colección.

 El siguiente tema proporciona más información sobre los errores de ADO.

-   [Errores de ADO](../../../ado/guide/data/ado-error-reference.md)
