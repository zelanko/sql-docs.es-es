---
title: Novedades de la integración CLR | Microsoft Docs
description: Microsoft SQL Server hospedar CLR se denomina integración CLR. En este artículo se describen las nuevas características de la integración CLR en SQL Server 2012.
ms.date: 03/03/2017
ms.prod: sql
ms.reviewer: ''
ms.custom: ''
ms.technology: clr
ms.topic: conceptual
ms.assetid: 871fcccd-b726-4b13-9f95-d02b4b39d8ab
author: rothja
ms.author: jroth
ms.openlocfilehash: eaf16cda98f019f6d378a3287e1068d78df88bac
ms.sourcegitcommit: 04cf7905fa32e0a9a44575a6f9641d9a2e5ac0f8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/07/2020
ms.locfileid: "91809521"
---
# <a name="clr-integration---what39s-new"></a>Integración de CLR: Qué&#39;s nuevo
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Las características siguientes son nuevas en la integración con CLR en [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]:  
  
-   En la versión 4 de CLR, los objetos de base de datos de CLR ya no detectan excepciones de estado dañado. Estas excepciones ahora se detectan en el nivel de hospedaje de la integración con CLR. Los componentes de la base de datos de CLR todavía pueden detectar estas excepciones mediante el establecimiento de un atributo de código ([ \<legacyCorruptedStateExceptionsPolicy> elemento](/dotnet/framework/configure-apps/file-schema/runtime/legacycorruptedstateexceptionspolicy-element)). Sin embargo, no se recomienda hacerlo porque los resultados no son confiables cuando se produce una excepción de estado dañado.  
  
-   Debido a los estrictos requisitos de seguridad de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], los componentes de la base de datos de CLR continuarán utilizando el modelo de seguridad de acceso del código definido en la versión 2.0 de CLR.  
  
-   En la versión 4 de CLR, un error de formato en un valor **System. TimeSpan** generará un **System. FormatExceptions**. Antes de la versión 4 de CLR, se omitió un error de formato en un valor **System. TimeSpan** . Las aplicaciones de base de datos que se basan en el comportamiento anterior a la versión 4 de CLR deben ejecutarse con un nivel de compatibilidad de base de datos (**nivel de compatibilidad de ALTER DATABASE**) de 100 o inferior. Para obtener más información, vea [<TimeSpan_LegacyFormatMode elemento>](/dotnet/framework/configure-apps/file-schema/runtime/timespan-legacyformatmode-element).  
  
-   La versión 4 de CLR admite Unicode 5.1. Las operaciones de ordenación relacionadas con algunos símbolos y signos de acentuación se verán mejoradas. Pueden producirse problemas de compatibilidad si la aplicación se basa en un comportamiento de ordenación heredado. Para habilitar la ordenación heredada, el nivel de compatibilidad de la base de datos (**nivel de compatibilidad de ALTER DATABASE**) debe establecerse en 100 o inferior. Para admitir esto, [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] instalará sort00001000.dll en el directorio de .NET Framework 4 (C:\Windows\Microsoft.NET\Framework\v4.0.30319). Para obtener más información, consulte [Elemento \<CompatSortNLSVersion>](/dotnet/framework/configure-apps/file-schema/runtime/compatsortnlsversion-element).  
  
-   Se han agregado las columnas siguientes a [Sys.dm_clr_appdomains](../../relational-databases/system-dynamic-management-views/sys-dm-clr-appdomains-transact-sql.md): **total_processor_time_ms**, **total_allocated_memory_kb**y **survived_memory_kb**.  
  
