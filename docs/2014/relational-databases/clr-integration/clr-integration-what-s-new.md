---
title: ¿Qué&#39;s de integración de CLR | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
ms.assetid: 871fcccd-b726-4b13-9f95-d02b4b39d8ab
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 2639697135e62b66dfd114eb74a7e918190c8fda
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48201835"
---
# <a name="what39s-new-in-clr-integration"></a>¿Qué&#39;s de integración CLR
  Las características siguientes son nuevas en la integración con CLR en [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]:  
  
-   En la versión 4 de CLR, los objetos de base de datos de CLR ya no detectan excepciones de estado dañado. Estas excepciones ahora se detectan en el nivel de hospedaje de la integración con CLR. Estas excepciones todavía se pueden detectar mediante los componentes de base de datos CLR estableciendo un atributo de código ([\<legacyCorruptedStateExceptionsPolicy > elemento](http://go.microsoft.com/fwlink/?LinkId=204954)). Sin embargo, no se recomienda hacerlo porque los resultados no son confiables cuando se produce una excepción de estado dañado.  
  
-   Debido a los estrictos requisitos de seguridad de [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)], los componentes de la base de datos de CLR continuarán utilizando el modelo de seguridad de acceso del código definido en la versión 2.0 de CLR.  
  
-   En la versión 4 de CLR, un error de formato en un valor `System.TimeSpan` generará `System.FormatExceptions`. Antes de la versión 4 de CLR, se omitían los errores de formato en los valores `System.TimeSpan`. Las aplicaciones de base de datos que dependen del comportamiento anterior a la versión 4 de CLR se deben ejecutar con un nivel de compatibilidad de la base de datos (`ALTER DATABASE Compatibility Level`) de 100 o inferior. Para obtener más información, consulte [< TimeSpan_LegacyFormatMode > elemento](http://go.microsoft.com/fwlink/?LinkId=205109).  
  
-   La versión 4 de CLR admite Unicode 5.1. Las operaciones de ordenación relacionadas con algunos símbolos y signos de acentuación se verán mejoradas. Pueden producirse problemas de compatibilidad si la aplicación se basa en un comportamiento de ordenación heredado. Para habilitar la ordenación heredada, el nivel de compatibilidad de la base de datos (`ALTER DATABASE Compatibility Level`) se debe establecer en 100 o inferior. Para admitir esto, [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] instalará sort00001000.dll en el directorio de .NET Framework 4 (C:\Windows\Microsoft.NET\Framework\v4.0.30319). Para obtener más información, consulte [ \<CompatSortNLSVersion > elemento](http://go.microsoft.com/fwlink/?LinkId=205110).  
  
-   Se han agregado las siguientes columnas a [sys.dm_clr_appdomains](/sql/relational-databases/system-dynamic-management-views/sys-dm-clr-appdomains-transact-sql): `total_processor_time_ms`, `total_allocated_memory_kb`, y `survived_memory_kb`.  
  
  
