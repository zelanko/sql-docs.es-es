---
title: Intercalación y los tipos de datos de integración de CLR | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: reference
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- data types [CLR integration]
- parameter collation [CLR integration]
- collations [CLR integration]
ms.assetid: 6ebaed8e-2e2b-4f6d-bf4b-bc25452de441
caps.latest.revision: 38
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 7c7d9f8cfe55a12237e2a2bf30b35ed1a57c5ec2
ms.sourcegitcommit: a78fa85609a82e905de9db8b75d2e83257831ad9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2018
ms.locfileid: "35694346"
---
# <a name="collation-and-clr-integration-data-types"></a>Intercalación y tipos de datos de integración CLR
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  En el [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)], **CompareInfo** objeto administra las intercalaciones. El [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] aplicación usan interfaces de programación (API) de la cadena la **CompareInfo** propiedad asociada con el **CultureInfo** objeto del subproceso actual para realizar comparaciones de cadenas. El valor predeterminado de la **CultureInfo** objeto se basa en el [!INCLUDE[msCoName](../../includes/msconame-md.md)] configuración regional de Windows para el equipo en el que [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está ejecutando. Esto determina la semántica de comparación predeterminada, si ya no explícita **CultureInfo** se especifica para las comparaciones de **System.String** valores. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] No cambie explícitamente el **CompareInfo** propiedad a la intercalación de base de datos o servidor. Si es necesario, los usuarios deben establecer adecuado **CompareInfo** propiedad en sus rutinas.  
  
## <a name="parameter-collation"></a>Intercalación de parámetros  
 Cuando se crea una rutina de common language runtime (CLR), y un parámetro de un método CLR se enlaza a la rutina es de tipo **SQLString**, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] crea una instancia del parámetro con la intercalación predeterminada de la base de datos que contiene la rutina que realiza la llamada. Si un parámetro no es un **SqlType** (por ejemplo, **cadena** en lugar de **SQLString**), la información de intercalación de la base de datos no está asociada con el parámetro.  
  
## <a name="see-also"></a>Vea también  
 [Tipos de datos de SQL Server en .NET Framework](../../relational-databases/clr-integration-database-objects-types-net-framework/sql-server-data-types-in-the-net-framework.md)  
  
  
