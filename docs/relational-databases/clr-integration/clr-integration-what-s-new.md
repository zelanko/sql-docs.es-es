---
title: "¿Qué &#39; s de integración CLR | Documentos de Microsoft"
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: clr
ms.reviewer: 
ms.suite: sql
ms.custom: 
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 871fcccd-b726-4b13-9f95-d02b4b39d8ab
caps.latest.revision: 
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4aaa1e92c83d16c951989a12f962fcfe45aec447
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/09/2018
---
# <a name="clr-integration---what39s-new"></a>Integración de CLR: ¿qué &#39; s nuevos
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
Las características siguientes son nuevas en la integración con CLR en [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]:  
  
-   En la versión 4 de CLR, los objetos de base de datos de CLR ya no detectan excepciones de estado dañado. Estas excepciones ahora se detectan en el nivel de hospedaje de la integración con CLR. Estas excepciones se seguirá detectando por los componentes de base de datos CLR estableciendo un atributo de código ([\<legacyCorruptedStateExceptionsPolicy > elemento](http://go.microsoft.com/fwlink/?LinkId=204954)). Sin embargo, no se recomienda hacerlo porque los resultados no son confiables cuando se produce una excepción de estado dañado.  
  
-   Debido a los estrictos requisitos de seguridad de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], los componentes de la base de datos de CLR continuarán utilizando el modelo de seguridad de acceso del código definido en la versión 2.0 de CLR.  
  
-   En CLR versión 4, un error de formato en un **System.TimeSpan** valor generará un **System.FormatExceptions**. Antes de la versión 4 de CLR, un error de formato en un **System.TimeSpan** se ignoró. Las aplicaciones de base de datos que se basan en el comportamiento anterior a la versión 4 de CLR deben ejecutar con un nivel de compatibilidad de base de datos (**nivel de compatibilidad de ALTER DATABASE**) de 100 o inferior. Para obtener más información, consulte [< TimeSpan_LegacyFormatMode > elemento](http://go.microsoft.com/fwlink/?LinkId=205109).  
  
-   La versión 4 de CLR admite Unicode 5.1. Las operaciones de ordenación relacionadas con algunos símbolos y signos de acentuación se verán mejoradas. Pueden producirse problemas de compatibilidad si la aplicación se basa en un comportamiento de ordenación heredado. Para habilitar la ordenación, el nivel de compatibilidad de base de datos heredada (**nivel de compatibilidad de ALTER DATABASE**) se debe establecer en 100 o inferior. Para admitir esto, [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] instalará sort00001000.dll en el directorio de .NET Framework 4 (C:\Windows\Microsoft.NET\Framework\v4.0.30319). Para obtener más información, consulte [ \<CompatSortNLSVersion > elemento](http://go.microsoft.com/fwlink/?LinkId=205110).  
  
-   Las columnas siguientes se agregaron a [sys.dm_clr_appdomains](../../relational-databases/system-dynamic-management-views/sys-dm-clr-appdomains-transact-sql.md): **total_processor_time_ms**, **total_allocated_memory_kb**, y **survived_ memory_kb**.  
  
  
