---
title: 'Paso 3: El servidor obtiene un conjunto de registros (Tutorial de RDS) | Microsoft Docs'
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS tutorial [ADO], server obtains Recordset
ms.assetid: 9c6779c9-1208-4696-ac51-c39f3a6d9240
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 15401f0121ead5125a96796a207a4a66f1ee9d1d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47727913"
---
# <a name="step-3-server-obtains-a-recordset-rds-tutorial"></a>Paso 3: el servidor obtiene un conjunto de registros (Tutorial de RDS)
El programa de servidor usa el texto de cadena y el comando connect para consultar el origen de datos para las filas deseadas. Normalmente se utiliza ADO para recuperar este **Recordset**, aunque otros datos de Microsoft acceder a las interfaces, tales como OLE DB, se puede usar.  
  
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, componentes de servidor RDS ya no están incluidos en el sistema operativo de Windows (consulte Windows 8 y [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obtener más detalles). Componentes de cliente RDS se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Deben migrar las aplicaciones que usan RDS a [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
 Un programa de servidor personalizado podría parecerse a esto:  
  
```  
Public Function ServerProgram(cn as String, qry as String) as Object  
Dim rs as New ADODB.Recordset  
   rs.CursorLocation = adUseClient  
   rs.Open qry, cn   
   rs.ActiveConnection = Nothing  
   Set ServerProgram = rs  
End Function  
```  
  
## <a name="see-also"></a>Vea también  
 [Paso 4: El servidor devuelve el conjunto de registros (Tutorial de RDS)](../../../ado/guide/remote-data-service/step-4-server-returns-the-recordset-rds-tutorial.md)   
 [Tutorial de RDS (VBScript)](../../../ado/guide/remote-data-service/rds-tutorial-vbscript.md)   
