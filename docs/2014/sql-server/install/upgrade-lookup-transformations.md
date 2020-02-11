---
title: Transformaciones de búsqueda de actualizaciones | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Lookup transformation and upgrading
- upgrading caching for Lookup transformation
- upgrading Lookup transformation
ms.assetid: d9b2c281-91ee-4e20-bdf0-0cd77d4a4241
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: eae7433569972c217161f1681b2f7089c7604335
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66091509"
---
# <a name="upgrade-lookup-transformations"></a>Actualizar las transformaciones de búsqueda
  Al actualizar de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] tiene la opción de modificar los paquetes para aprovechar las nuevas características de la transformación Búsqueda. La transformación admite los tipos de almacenamiento en memoria caché y las opciones de salida de datos disponibles en [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)]. Para obtener más información sobre el almacenamiento en caché y las salidas de datos, vea [transformación búsqueda](../../integration-services/data-flow/transformations/lookup-transformation.md).  
  
 En [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)], los tipos de almacenamiento en caché disponibles son almacenamiento en caché completo, almacenamiento parcial y ningún almacenamiento en caché. En [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)], puede configurar una transformación de Búsqueda para utilizar uno de estos tipos de almacenamiento en caché. Para obtener más información sobre cómo implementar almacenamiento en caché parcial o sin almacenamiento en caché, vea [implementar una búsqueda en modo no hay caché o caché parcial](../../integration-services/data-flow/transformations/implement-a-lookup-in-no-cache-or-partial-cache-mode.md). Para obtener información sobre cómo implementar el almacenamiento en caché completo, vea [implementar una transformación de búsqueda en el modo de caché completa mediante el administrador de conexiones de caché](../../integration-services/connection-manager/lookup-transformation-full-cache-mode-cache-connection-manager.md) e [implementar una transformación búsqueda en el modo de caché completa mediante el administrador de conexiones de OLE DB](../../integration-services/connection-manager/lookup-transformation-full-cache-mode-ole-db-connection-manager.md).  
  
 En [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)], la transformación Búsqueda tenía una entrada, una salida y una salida de error. Las filas del contenido de entrada que tenían entradas coincidentes se controlaron en el resultado de salida. Las filas del contenido de entrada que no tenían entradas coincidentes se trataron como errores y se pudieron redirigir a la salida de error. En [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)], la transformación Búsqueda tiene dos resultados: un resultado coincidente y otro no coincidente.  
  
 De forma predeterminada, al ejecutar una transformación Búsqueda creada en [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] trata las filas sin entradas coincidentes como errores y permite redirigir las filas a una salida de error. Tiene la opción de configurar la transformación Búsqueda para tratar las filas como no errores y redirigir las filas al resultado no coincidente.  
  
 Para obtener más información, vea [Editor de transformación búsqueda &#40;página General&#41;](../../integration-services/general-page-of-integration-services-designers-options.md).  
  
## <a name="see-also"></a>Consulte también  
 [Transformación Búsqueda](../../integration-services/data-flow/transformations/lookup-transformation.md)  
  
  
