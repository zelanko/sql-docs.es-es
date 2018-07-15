---
title: Intercalación y tipos de datos de integración de CLR | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: clr
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
ms.openlocfilehash: 31bb87caa5d5b997c3e99478fc3308fc03d4f956
ms.sourcegitcommit: 022d67cfbc4fdadaa65b499aa7a6a8a942bc502d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/03/2018
ms.locfileid: "37357707"
---
# <a name="collation-and-clr-integration-data-types"></a>Intercalación y tipos de datos de integración CLR
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  En el [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)], **CompareInfo** objeto administra las intercalaciones. El [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] aplicación utilizan interfaces de programación (API) de la cadena la **CompareInfo** propiedad asociada con el **CultureInfo** objetos del subproceso actual para realizar comparaciones de cadenas. El valor predeterminado de la **CultureInfo** objeto se basa en el [!INCLUDE[msCoName](../../includes/msconame-md.md)] configuración regional de Windows para el equipo en el que [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se está ejecutando. Esto determina la semántica de comparación predeterminada, si no explícita **CultureInfo** se especifica para las comparaciones de **System.String** valores. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] No cambie explícitamente la **CompareInfo** propiedad a la intercalación de base de datos o servidor. Si es necesario, los usuarios deben establecer adecuado **CompareInfo** propiedad en sus rutinas.  
  
## <a name="parameter-collation"></a>Intercalación de parámetros  
 Cuando se crea una rutina de common language runtime (CLR), y un parámetro de un método CLR enlaza a la rutina es de tipo **SQLString**, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] crea una instancia del parámetro con la intercalación predeterminada de la base de datos que contiene la rutina de llamada. Si un parámetro no es un **SqlType** (por ejemplo, **cadena** lugar **SQLString**), la información de intercalación de la base de datos no está asociada con el parámetro.  
  
## <a name="see-also"></a>Vea también  
 [Tipos de datos de SQL Server en .NET Framework](../../relational-databases/clr-integration-database-objects-types-net-framework/sql-server-data-types-in-the-net-framework.md)  
  
  
