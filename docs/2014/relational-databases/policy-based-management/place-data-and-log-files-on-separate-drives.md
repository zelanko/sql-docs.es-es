---
title: Colocación de los datos y los archivos de registro en unidades independientes | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 6cbedc27-4d77-44ad-bed2-c23b628475a7
caps.latest.revision: 7
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 15cef6ec95e32d1eb086f7695b8f62e314cbc65c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36104675"
---
# <a name="place-data-and-log-files-on-separate-drives"></a>Colocar los datos y los archivos de registro en unidades independientes
  Esta regla comprueba si los datos y archivos de registro se colocan en unidades lógicas independientes. Al colocar tanto los archivos de registro como los datos en el mismo dispositivo, se puede ocasionar la contención por ese dispositivo y provocar un rendimiento escaso. Colocar los archivos en unidades de disco independientes permite que la actividad de E/S tenga lugar al mismo tiempo para los archivos de registro y los datos.  
  
## <a name="best-practices-recommendations"></a>Prácticas recomendadas  
 Al crear una base de datos nueva, especifique unidades independientes para los datos y el registro. Para mover los archivos una vez creada la base de datos, esta debe ponerse sin conexión. Mover los archivos mediante uno de los métodos siguientes:  
  
> [!NOTE]  
>  Esta directiva no puede detectar dispositivos físicos independientes mediante puntos de montaje  
  
-   Restaure la base de datos a partir de la copia de seguridad utilizando la instrucción RESTORE DATABASE con la opción WITH MOVE.  
  
-   Desasocie y, a continuación, asocie la base de datos especificando ubicaciones independientes para los datos y los dispositivos de registro.  
  
-   Especifique una ubicación nueva ejecutando la instrucción ALTER DATABASE con la opción MODIFY FILE y reiniciando a continuación la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="for-more-information"></a>Para obtener más información  
 [Mover archivos de base de datos](../databases/move-database-files.md)  
  
 [Mover bases de datos de usuario](../databases/move-user-databases.md)  
  
 [Adjuntar y separar bases de datos &#40;SQL Server&#41;](../databases/database-detach-and-attach-sql-server.md)  
  
## <a name="see-also"></a>Vea también  
 [Supervisar y aplicar las prácticas recomendadas usando la administración basada en directivas](monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  