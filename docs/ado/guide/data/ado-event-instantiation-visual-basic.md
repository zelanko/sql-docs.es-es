---
title: 'Creación de instancias de eventos de ADO: Visual Basic | Microsoft Docs'
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- VB
ms.assetid: dce0a2a3-326f-4aaf-a822-6c5549833afa
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c0223d4d4346f26ff9339fce3cbc43be9bfcbe82
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47772483"
---
# <a name="ado-event-instantiation-visual-basic"></a>Creación de instancias de eventos de ADO: Visual Basic
Para controlar eventos de ADO en Microsoft® Visual Basic®, se debe declarar una variable nivel de módulo mediante la **WithEvents** palabra clave. La variable se puede declarar únicamente como parte de un módulo de clase y se debe declarar en el nivel de módulo. Esto no es tan restrictivo como parece, sin embargo, dado que Visual Basic **formulario** objetos también son clases. La manera más sencilla de controlar eventos de ADO es declarar una variable utilizando **WithEvents**. El ejemplo siguiente se controla el **ConnectComplete** eventos para un **conexión** objeto:  
  
```  
' BeginEventExampleVB02  
Dim WithEvents connEvent As Connection  
Attribute connEvent.VB_VarHelpID = -1  
  
Private Sub Form_Load()  
Dim strConn As String  
  
   ' Create a new object with event  
   ' handling enabled.  
   strConn = "Provider=sqloledb;" & _  
      "Data Source=MyServer;" & _  
      "Initial Catalog=Northwind;" & _  
      "Integrated Security=SSPI;"  
   Set connEvent = New ADODB.Connection  
   connEvent.Open strConn  
End Sub  
  
Private Sub connEvent_ConnectComplete(ByVal pError As ADODB.Error, _  
    adStatus As ADODB.EventStatusEnum, _  
    ByVal pConnection As ADODB.Connection)  
Dim strMsg As String  
  
   If adStatus = adStatusErrorsOccurred Then  
      Select Case pError.Number  
         Case adErrOperationCancelled  
            ' The operation was cancelled in the  
            ' Will event. Notify the user and exit.  
            strMsg = "I'm sorry you can't connect right now." & vbCrLf  
            strMsg = strMsg & "Click OK to exit."  
            Unload Me  
         Case Else  
            strMsg = "Error " & Format(pError.Number) & vbCrLf  
            strMsg = strMsg & pError.Description  
            strMsg = strMsg & "Click OK to exit."  
            Unload Me  
      End Select  
   End If  
   frmWait.btnOK.Enabled = True  
End Sub  
' EndEventExampleVB02  
```  
  
 El **conexión** objeto se declara en el **formulario** nivel mediante el **WithEvents** palabra clave para habilitar el control de eventos. El controlador de eventos Form_Load crea el objeto asignando un nuevo **conexión** objeto *connEvent* y, a continuación, abre la conexión. Por supuesto, una aplicación real realizará más procesamiento en el controlador de eventos Form_Load que se muestra aquí.
