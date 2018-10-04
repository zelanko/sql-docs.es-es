---
title: 'Paso 1: Especificar un programa de servidor (Tutorial de RDS) | Microsoft Docs'
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS tutorial [ADO], specifying server program
ms.assetid: d8bb35b1-c02a-4231-8d55-016e56e53b95
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8dd842dd689b8aa15203f0918c44b7047831bb93
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47732273"
---
# <a name="step-1-specify-a-server-program-rds-tutorial"></a>Paso 1: especificar un programa de servidor (Tutorial de RDS)
En el caso más general, utilice el [RDS. DataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md) objeto [CreateObject](../../../ado/reference/rds-api/createobject-method-rds.md) método para especificar el programa de servidor predeterminado, [RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md), o su propio programa de servidor personalizado (objeto de negocios). Se crea una instancia de un programa de servidor en el servidor y una referencia al programa de servidor, o *proxy*, se devuelve.  
  
 Este tutorial usa el programa de servidor predeterminado:  
  
```  
Sub RDSTutorial1()  
   Dim DS as New RDS.DataSpace  
   Dim DF as Object  
   Set DF = DS.("RDSServer.DataFactory", "http://yourServer")  
...  
```  
  
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, componentes de servidor RDS ya no están incluidos en el sistema operativo de Windows (consulte Windows 8 y [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obtener más detalles). Componentes de cliente RDS se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Deben migrar las aplicaciones que usan RDS a [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="see-also"></a>Vea también  
 [Paso 2: Invocar el programa de servidor (Tutorial de RDS)](../../../ado/guide/remote-data-service/step-2-invoke-the-server-program-rds-tutorial.md)   
 [Tutorial de RDS (VBScript)](../../../ado/guide/remote-data-service/rds-tutorial-vbscript.md)   
