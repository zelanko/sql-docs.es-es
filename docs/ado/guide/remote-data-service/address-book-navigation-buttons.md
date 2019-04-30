---
title: Botones de navegación de la libreta de direcciones | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS scenarios [ADO], navigation buttons
- address book application scenario [ADO], navigation buttons
ms.assetid: f0dd84c6-5c33-4ab9-82b4-4c42dfdd2277
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 60d3b2660f3a20883e9b9f2d3b4202526c15a943
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63242785"
---
# <a name="address-book-navigation-buttons"></a>Botones de navegación de la libreta de direcciones
La aplicación de la libreta de direcciones muestra los botones de navegación en la parte inferior de la página Web. Puede usar los botones de navegación para navegar por los datos de la presentación de la cuadrícula HTML seleccionando la primera o última fila de datos o las filas adyacentes a la selección actual.  
  
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, componentes de servidor RDS ya no están incluidos en el sistema operativo de Windows (consulte Windows 8 y [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obtener más detalles). Componentes de cliente RDS se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Deben migrar las aplicaciones que usan RDS a [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="navigation-sub-procedures"></a>Subprocedimientos de navegación  
 La aplicación de la libreta de direcciones contiene varios procedimientos que permiten a los usuarios hacer clic en el **primera**, **siguiente**, **anterior**, y **última** botones para desplazarse por los datos.  
  
 Por ejemplo, al hacer clic en el **primera** botón activa el procedimiento Sub First_OnClick de VBScript. El procedimiento se ejecuta un [MoveFirst](../../../ado/reference/rds-api/movefirst-movelast-movenext-and-moveprevious-methods-rds.md) método, lo que hace que la primera fila de datos de la selección actual. Al hacer clic en el **última** botón activa el procedimiento Sub Last_OnClick, que invoca la [MoveLast](../../../ado/reference/rds-api/movefirst-movelast-movenext-and-moveprevious-methods-rds.md) método, que realiza la última fila de datos de la selección actual. Los botones de navegación restantes funcionan de manera similar.  
  
```vb
' Move to the first record in the bound Recordset.  
Sub First_OnClick  
   DC1.Recordset.MoveFirst  
End Sub  
  
' Move to the next record from the current position   
' in the bound Recordset.  
Sub Next_OnClick  
   If Not DC1.Recordset.EOF Then    ' Cannot move beyond bottom record.  
      DC1.Recordset.MoveNext  
      Exit Sub  
   End If     
End Sub  
  
' Move to the previous record from the current position in the bound   
' Recordset.  
Sub Prev_OnClick  
   If Not DC1.Recordset.BOF Then    ' Cannot move beyond top record.  
      DC1.Recordset.MovePrevious  
      Exit Sub  
   End If  
End Sub  
  
' Move to the last record in the bound Recordset.  
Sub Last_OnClick  
   DC1.Recordset.MoveLast  
End Sub  
```  
  
## <a name="see-also"></a>Vea también  
 [Objeto DataControl (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)   
 [MoveFirst, MoveLast, MoveNext y MovePrevious métodos (RDS)](../../../ado/reference/rds-api/movefirst-movelast-movenext-and-moveprevious-methods-rds.md)



