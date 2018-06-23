---
title: ¿Qué&#39;s de integración CLR | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 871fcccd-b726-4b13-9f95-d02b4b39d8ab
caps.latest.revision: 6
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 5cc1f1674a4704ad156212744025ec1d98422a24
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36107215"
---
# <a name="what39s-new-in-clr-integration"></a>¿Qué&#39;s de integración CLR
  Las características siguientes son nuevas en la integración con CLR en [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]:  
  
-   En la versión 4 de CLR, los objetos de base de datos de CLR ya no detectan excepciones de estado dañado. Estas excepciones ahora se detectan en el nivel de hospedaje de la integración con CLR. Estas excepciones se seguirá detectando por los componentes de base de datos CLR estableciendo un atributo de código ([\<legacyCorruptedStateExceptionsPolicy > elemento](http://go.microsoft.com/fwlink/?LinkId=204954)). Sin embargo, no se recomienda hacerlo porque los resultados no son confiables cuando se produce una excepción de estado dañado.  
  
-   Debido a los estrictos requisitos de seguridad de [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)], los componentes de la base de datos de CLR continuarán utilizando el modelo de seguridad de acceso del código definido en la versión 2.0 de CLR.  
  
-   En la versión 4 de CLR, un error de formato en un valor `System.TimeSpan` generará `System.FormatExceptions`. Antes de la versión 4 de CLR, se omitían los errores de formato en los valores `System.TimeSpan`. Las aplicaciones de base de datos que dependen del comportamiento anterior a la versión 4 de CLR se deben ejecutar con un nivel de compatibilidad de la base de datos (`ALTER DATABASE Compatibility Level`) de 100 o inferior. Para obtener más información, consulte [< TimeSpan_LegacyFormatMode > elemento](http://go.microsoft.com/fwlink/?LinkId=205109).  
  
-   La versión 4 de CLR admite Unicode 5.1. Las operaciones de ordenación relacionadas con algunos símbolos y signos de acentuación se verán mejoradas. Pueden producirse problemas de compatibilidad si la aplicación se basa en un comportamiento de ordenación heredado. Para habilitar la ordenación heredada, el nivel de compatibilidad de la base de datos (`ALTER DATABASE Compatibility Level`) se debe establecer en 100 o inferior. Para admitir esto, [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] instalará sort00001000.dll en el directorio de .NET Framework 4 (C:\Windows\Microsoft.NET\Framework\v4.0.30319). Para obtener más información, consulte [ \<CompatSortNLSVersion > elemento](http://go.microsoft.com/fwlink/?LinkId=205110).  
  
-   Las columnas siguientes se agregaron a [sys.dm_clr_appdomains](/sql/relational-databases/system-dynamic-management-views/sys-dm-clr-appdomains-transact-sql): `total_processor_time_ms`, `total_allocated_memory_kb`, y `survived_memory_kb`.  
  
  
