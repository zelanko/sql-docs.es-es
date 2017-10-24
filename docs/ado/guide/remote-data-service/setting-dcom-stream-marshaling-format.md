---
title: "Establecer el formato de serialización de secuencias de DCOM | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- dcom stream marshaling format in rds [ADO]
ms.assetid: 46664ac5-d6e6-4457-8bae-3a98300f2a41
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: abc77e2e56ec8251e158121ca8bb6083641d4cb3
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="setting-dcom-stream-marshaling-format"></a>Establecer el formato de serialización de secuencias de DCOM
Un equipo cliente mediante componentes de RDS 1.5 o versiones anteriores no es compatible con un servidor mediante componentes de RDS 2.0 o posterior. Cuando se utiliza DCOM como protocolo subyacente, la compatibilidad con RDS 2.0 o posterior es más eficaz en el transporte [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objetos. Si el cliente está ejecutando componentes de RDS 1.5 o versiones anteriores, puede configurar el servidor para que funcione con la compatibilidad RDS anterior (denominada RDS 1.0) o la nueva compatibilidad RDS (denominada RDS 2.0 o posterior). Establezca cualquiera de las entradas del registro siguientes:  
  
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, componentes de servidor RDS ya no están incluidos en el sistema operativo Windows (consulte Windows 8 y [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obtener más detalles). Componentes de cliente RDS se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Las aplicaciones que utilizan RDS deben migrar a [servicio de datos de WCF](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
```  
[HKEY_CLASSES_ROOT]  
\CLSID\[58ECEE30-E715-11CF-B0E3-00AA003F000F}\ADTGOptions]"MarshalFormat"="RDS10"  
```  
  
 -O bien-  
  
```  
[HKEY_CLASSES_ROOT]  
\CLSID\[58ECEE30-E715-11CF-B0E3-00AA003F000F}\ADTGOptions]"MarshalFormat"="RDS20"  
```



