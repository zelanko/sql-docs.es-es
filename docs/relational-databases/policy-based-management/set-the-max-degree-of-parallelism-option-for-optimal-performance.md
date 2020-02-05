---
title: Grado máximo de paralelismo y administración basada en directivas
description: Describe cómo configurar una directiva para comprobar el valor de grado máximo de paralelismo para la administración basada en directivas para SQL Server.
ms.custom: seo-lt-2019
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: ec908006-67ae-4674-9a61-25ea741d6197
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: a03a0236c177605bf5041e92ea9c19708d5bc9ae
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "75776372"
---
# <a name="set-the-max-degree-of-parallelism-option-for-optimal-performance"></a>Establecer la opción Grado máximo de paralelismo para lograr un rendimiento óptimo
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Esta regla determina si la opción Grado máximo de paralelismo (MAXDOP) tiene un valor mayor que 8. Establecer esta opción en un valor mayor a menudo causa un consumo de recursos no deseado y la degradación del rendimiento.  
  
## <a name="best-practice-recommendations"></a>Mejores prácticas recomendadas  
 La opción de configuración de grado máximo de paralelismo (MAXDOP) controla el número de procesadores que se usan para la ejecución de una consulta en un plan paralelo. Esta opción determina el número de subprocesos que se usan para los operadores de plan de consulta que realizan el trabajo en paralelo. Dependiendo de si SQL Server está configurado en un equipo con multiproceso simétrico (SMP), un equipo de acceso a memoria no uniforme (NUMA) o procesadores habilitados para hyperthreading, tendrá que configurar correctamente la opción de grado máximo de paralelismo. 
 
 Las recomendaciones para configurar MAXDOP dependen de la versión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que se esté usando. Para obtener instrucciones específicas de la versión, vea [Establecer la opción de configuración del servidor Grado máximo de paralelismo](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md#Guidelines) y configure la directiva para comprobar en consonancia el valor de grado máximo de paralelismo.     
  
## <a name="for-more-information"></a>Para obtener más información  
 [Recomendaciones y directrices para la opción de configuración "grado máximo de paralelismo" en SQL Server](https://go.microsoft.com/fwlink/?linkid=117786)    
 [Establecer la opción de configuración del servidor Grado máximo de paralelismo](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md#Guidelines)     
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)     
  
