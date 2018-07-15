---
title: ¿Qué&#39;s de integración de CLR | Microsoft Docs
ms.date: 03/03/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.custom: ''
ms.technology: clr
ms.topic: conceptual
ms.assetid: 871fcccd-b726-4b13-9f95-d02b4b39d8ab
caps.latest.revision: 7
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 55cb6537db540fb5d916b72cb1b469dc3846f419
ms.sourcegitcommit: 022d67cfbc4fdadaa65b499aa7a6a8a942bc502d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/03/2018
ms.locfileid: "37356217"
---
# <a name="clr-integration---what39s-new"></a>Integración de CLR: ¿qué&#39;s nuevo
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Las características siguientes son nuevas en la integración con CLR en [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]:  
  
-   En la versión 4 de CLR, los objetos de base de datos de CLR ya no detectan excepciones de estado dañado. Estas excepciones ahora se detectan en el nivel de hospedaje de la integración con CLR. Estas excepciones todavía se pueden detectar mediante los componentes de base de datos CLR estableciendo un atributo de código ([\<legacyCorruptedStateExceptionsPolicy > elemento](http://go.microsoft.com/fwlink/?LinkId=204954)). Sin embargo, no se recomienda hacerlo porque los resultados no son confiables cuando se produce una excepción de estado dañado.  
  
-   Debido a los estrictos requisitos de seguridad de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], los componentes de la base de datos de CLR continuarán utilizando el modelo de seguridad de acceso del código definido en la versión 2.0 de CLR.  
  
-   En CLR versión 4, un error de formato en un **System.TimeSpan** valor generará un **System.FormatExceptions**. Antes de la versión 4 de CLR, un error de formato en un **System.TimeSpan** se ignoró. Las aplicaciones de base de datos que dependen del comportamiento antes de la versión 4 de CLR deben ejecutarse con un nivel de compatibilidad de base de datos (**nivel de compatibilidad de ALTER DATABASE**) de 100 o inferior. Para obtener más información, consulte [< TimeSpan_LegacyFormatMode > elemento](http://go.microsoft.com/fwlink/?LinkId=205109).  
  
-   La versión 4 de CLR admite Unicode 5.1. Las operaciones de ordenación relacionadas con algunos símbolos y signos de acentuación se verán mejoradas. Pueden producirse problemas de compatibilidad si la aplicación se basa en un comportamiento de ordenación heredado. Para habilitar la ordenación, el nivel de compatibilidad de base de datos heredada (**nivel de compatibilidad de ALTER DATABASE**) se debe establecer en 100 o menos. Para admitir esto, [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] instalará sort00001000.dll en el directorio de .NET Framework 4 (C:\Windows\Microsoft.NET\Framework\v4.0.30319). Para obtener más información, consulte [ \<CompatSortNLSVersion > elemento](http://go.microsoft.com/fwlink/?LinkId=205110).  
  
-   Se han agregado las siguientes columnas a [sys.dm_clr_appdomains](../../relational-databases/system-dynamic-management-views/sys-dm-clr-appdomains-transact-sql.md): **total_processor_time_ms**, **total_allocated_memory_kb**, y **survived_ memory_kb**.  
  
  
