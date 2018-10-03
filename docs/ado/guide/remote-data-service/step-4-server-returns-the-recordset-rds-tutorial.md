---
title: 'Paso 4: El servidor devuelve el conjunto de registros (Tutorial de RDS) | Microsoft Docs'
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS tutorial [ADO], server returns Recordset
ms.assetid: 3d1855c4-419c-4810-b5ea-6c874b5e2905
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2edc9b1e0a235f10819f319cc68a595610a4e5d9
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47783903"
---
# <a name="step-4-server-returns-the-recordset-rds-tutorial"></a>Paso 4: el servidor devuelve el conjunto de registros (Tutorial de RDS)
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, componentes de servidor RDS ya no están incluidos en el sistema operativo de Windows (consulte Windows 8 y [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obtener más detalles). Componentes de cliente RDS se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Deben migrar las aplicaciones que usan RDS a [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
 RDS convierte el objeto recuperado **conjunto de registros** objeto a un formulario que se puede enviar al cliente (es decir, que *serializa* el **Recordset**). La forma exacta de la conversión y cómo se envía depende de si el servidor está en Internet o una intranet, una red de área local, o es una biblioteca de vínculos dinámicos. Sin embargo, este detalle no es crítico; todo lo que importa es que RDS envía el **Recordset** al cliente.  
  
 En el lado cliente, un **Recordset** objeto se devuelve y se asigna a una variable local.  
  
```  
Sub RDSTutorial4()  
   Dim DS as New RDS.DataSpace  
   Dim RS as ADODB.Recordset  
   Dim DF as Object  
   Set DF = DS.CreateObject("RDSServer.DataFactory", "http://yourServer")  
   Set RS = DF.Query("DSN=Pubs", "SELECT * FROM Authors")  
...  
```  
  
## <a name="see-also"></a>Vea también  
 [Paso 5: Control de datos es realizado utilizable (Tutorial de RDS)](../../../ado/guide/remote-data-service/step-5-datacontrol-is-made-usable-rds-tutorial.md)   
 [Tutorial de RDS (VBScript)](../../../ado/guide/remote-data-service/rds-tutorial-vbscript.md)   
