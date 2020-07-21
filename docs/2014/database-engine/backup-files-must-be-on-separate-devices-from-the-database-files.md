---
title: Los archivos de copia de seguridad deben estar en dispositivos independientes de los archivos de base de datos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 7039bebb-1f25-4cf3-81f1-393dfb78da12
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: d5eff9cb3139e1e1043f99ba63d11160b1010c27
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84936150"
---
# <a name="backup-files-must-be-on-separate-devices-from-the-database-files"></a>Los archivos de copia de seguridad deben estar en dispositivos independientes de los archivos de base de datos
  Esta regla comprueba si los archivos de base de datos están en dispositivos independientes de los archivos de copia de seguridad. Si los archivos de base de datos y los archivos de copia de seguridad están en el mismo dispositivo y este sufre un error, la base de datos y las copias de seguridad no estarán disponibles. Además, al colocar los archivos de base de datos y los archivos de copia de seguridad en dispositivos independientes, mejora el rendimiento de E/S en el uso en producción de la base de datos y en la escritura de las copias de seguridad.  
  
## <a name="best-practices-recommendations"></a>Prácticas recomendadas  
 Recomendamos encarecidamente que la base de datos y las copias de seguridad se coloquen en dispositivos de copia de seguridad independientes.  
  
> [!NOTE]  
>  Esta directiva no puede detectar dispositivos físicos independientes mediante puntos de montaje.  
  
## <a name="for-more-information"></a>Para obtener más información  
 [Dispositivos de copia de seguridad &#40;SQL Server&#41;](../relational-databases/backup-restore/backup-devices-sql-server.md)  
  
 [Copia de seguridad y restauración de bases de datos de SQL Server](../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)  
  
## <a name="see-also"></a>Consulte también  
 [Supervisar y aplicar las prácticas recomendadas usando la administración basada en directivas](../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
