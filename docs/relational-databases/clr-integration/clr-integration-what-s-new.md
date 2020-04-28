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
ms.openlocfilehash: d27bf0d925d3a98dda488fb85aff7446434cc8ad
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81488096"
---
# <a name="clr-integration---what39s-new"></a>Integración de CLR: Qué&#39;s nuevo
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Las características siguientes son nuevas en la integración con CLR en [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]:  
  
-   En la versión 4 de CLR, los objetos de base de datos de CLR ya no detectan excepciones de estado dañado. Estas excepciones ahora se detectan en el nivel de hospedaje de la integración con CLR. Los componentes de la base de datos de CLR todavía pueden detectar estas excepciones mediante el establecimiento de un atributo de código ([\<legacyCorruptedStateExceptionsPolicy> elemento](https://go.microsoft.com/fwlink/?LinkId=204954)). Sin embargo, no se recomienda hacerlo porque los resultados no son confiables cuando se produce una excepción de estado dañado.  
  
-   Debido a los estrictos requisitos de seguridad de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], los componentes de la base de datos de CLR continuarán utilizando el modelo de seguridad de acceso del código definido en la versión 2.0 de CLR.  
  
-   En la versión 4 de CLR, un error de formato en un valor **System. TimeSpan** generará un **System. FormatExceptions**. Antes de la versión 4 de CLR, se omitió un error de formato en un valor **System. TimeSpan** . Las aplicaciones de base de datos que se basan en el comportamiento anterior a la versión 4 de CLR deben ejecutarse con un nivel de compatibilidad de base de datos (**nivel de compatibilidad de ALTER DATABASE**) de 100 o inferior. Para obtener más información, vea [<TimeSpan_LegacyFormatMode elemento>](https://go.microsoft.com/fwlink/?LinkId=205109).  
  
-   La versión 4 de CLR admite Unicode 5.1. Las operaciones de ordenación relacionadas con algunos símbolos y signos de acentuación se verán mejoradas. Pueden producirse problemas de compatibilidad si la aplicación se basa en un comportamiento de ordenación heredado. Para habilitar la ordenación heredada, el nivel de compatibilidad de la base de datos (**nivel de compatibilidad de ALTER DATABASE**) debe establecerse en 100 o inferior. Para admitir esto, [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] instalará sort00001000.dll en el directorio de .NET Framework 4 (C:\Windows\Microsoft.NET\Framework\v4.0.30319). Para obtener más información, vea [ \<CompatSortNLSVersion> elemento](https://go.microsoft.com/fwlink/?LinkId=205110).  
  
-   Se han agregado las columnas siguientes a [Sys. dm_clr_appdomains](../../relational-databases/system-dynamic-management-views/sys-dm-clr-appdomains-transact-sql.md): **total_processor_time_ms**, **total_allocated_memory_kb**y **survived_memory_kb**.  
  
  
