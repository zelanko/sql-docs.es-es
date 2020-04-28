---
title: Intercalación y tipos de datos de integración CLR | Microsoft Docs
description: En la integración de CLR de SQL Server, las API de cadena de .NET Framework usan la propiedad CompareInfo de CultureInfo del subproceso actual para realizar comparaciones de cadenas.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- data types [CLR integration]
- parameter collation [CLR integration]
- collations [CLR integration]
ms.assetid: 6ebaed8e-2e2b-4f6d-bf4b-bc25452de441
author: rothja
ms.author: jroth
ms.openlocfilehash: 46e4d450db90e4bfc93187a48ca8adae472036c6
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81488501"
---
# <a name="collation-and-clr-integration-data-types"></a>Intercalación y tipos de datos de integración CLR
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  En [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)], el objeto **CompareInfo** controla las intercalaciones. Las [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] interfaces de programación de aplicaciones (API) de cadenas utilizan la propiedad **CompareInfo** asociada al objeto **CultureInfo** del subproceso actual para realizar comparaciones de cadenas. La configuración predeterminada del objeto **CultureInfo** se basa en la [!INCLUDE[msCoName](../../includes/msconame-md.md)] configuración regional de Windows del equipo en el que [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se está ejecutando. Esto determina la semántica de comparación predeterminada, si no se especifica **CultureInfo** explícito, para las comparaciones de valores **System. String** . [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]no cambia explícitamente la propiedad **CompareInfo** a la intercalación de base de datos o servidor. Si es necesario, los usuarios deben establecer la propiedad **CompareInfo** adecuada en sus rutinas.  
  
## <a name="parameter-collation"></a>Intercalación de parámetros  
 Cuando se crea una rutina de Common Language Runtime (CLR) y un parámetro de un método CLR enlazado a la rutina es de **SQLString**tipo SQLString [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , crea una instancia del parámetro con la intercalación predeterminada de la base de datos que contiene la rutina de llamada. Si un parámetro no es un **SqlType** (por ejemplo, **String** en lugar de **SQLString**), la información de intercalación de la base de datos no está asociada al parámetro.  
  
## <a name="see-also"></a>Consulte también  
 [Tipos de datos de SQL Server en .NET Framework](../../relational-databases/clr-integration-database-objects-types-net-framework/sql-server-data-types-in-the-net-framework.md)  
  
  
