---
title: Ejemplo de la propiedad de controlador (VB) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- VB
helpviewer_keywords:
- Handler property [ADO], Visual Basic example
ms.assetid: 9664f9a6-65fc-4e7f-be3d-3e4b501b558a
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 657f266ab4bcc6e03a645bcfc3d4f914c5fa6259
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66712717"
---
# <a name="handler-property-example-vb"></a>Ejemplo de la propiedad de controlador (VB)
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, componentes de servidor RDS ya no están incluidos en el sistema operativo de Windows (consulte Windows 8 y [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obtener más detalles). Componentes de cliente RDS se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Deben migrar las aplicaciones que usan RDS a [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
 Este ejemplo se muestra el [RDS DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) objeto [controlador](../../../ado/reference/rds-api/handler-property-rds.md) propiedad. (Consulte [personalización de DataFactory](../../../ado/guide/remote-data-service/datafactory-customization.md) para obtener más detalles.)  
  
 Supongamos que las siguientes secciones del archivo de parámetros, Msdfmap.ini, se encuentran en el servidor:  
  
```  
[connect AuthorDataBase]  
Access=ReadWrite  
Connect="DSN=Pubs"  
[sql AuthorById]  
SQL="SELECT * FROM Authors WHERE au_id = ?"  
```  
  
 El código tiene el siguiente aspecto. El comando asignado a la [SQL](../../../ado/reference/rds-api/sql-property.md) coincidirá con la propiedad la ***AuthorById*** identificador y recuperará una fila por Michael O'Leary autor. El **DataControl** objeto **Recordset** propiedad se asigna a un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto únicamente como una comodidad de codificación.  
  
```  
'BeginHandlerVB  
Public Sub Main()  
    On Error GoTo ErrorHandler  
  
    Dim dc As New DataControl  
    Dim rst As ADODB.Recordset  
  
    dc.Handler = "MSDFMAP.Handler"  
    dc.ExecuteOptions = 1  
    dc.FetchOptions = 1  
    dc.Server = "https://MyServer"  
    dc.Connect = "Data Source=AuthorDataBase"  
    dc.SQL = "AuthorById('267-41-2394')"  
    dc.Refresh                  'Retrieve the record  
    Set rst = dc.Recordset      'Use another Recordset as a convenience  
    Debug.Print "Author is '" & rst!au_fname & " " & rst!au_lname & "'"  
  
    ' clean up  
    If rst.State = adStateOpen Then rst.Close  
    Set rst = Nothing  
    Set dc = Nothing  
    Exit Sub  
  
ErrorHandler:  
    ' clean up  
    If Not rst Is Nothing Then  
        If rst.State = adStateOpen Then rst.Close  
    End If  
    Set rst = Nothing  
    Set dc = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
'EndHandlerVB  
```  
  
## <a name="see-also"></a>Vea también  
 [Objeto DataControl (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)   
 [Propiedad de controlador (RDS)](../../../ado/reference/rds-api/handler-property-rds.md)


