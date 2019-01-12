---
title: Ubicaciones alternativas para las carpetas de instantáneas | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- snapshots [SQL Server replication], alternate folder locations
- snapshot replication [SQL Server], alternate folder locations
- alternate snapshot folders [SQL Server replication]
ms.assetid: 437553b0-19df-4522-8f27-06b5bc747c69
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c86e79928bdadb129ed0aa591e4bd035ffe22c1c
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/09/2019
ms.locfileid: "54129005"
---
# <a name="alternate-snapshot-folder-locations"></a>Ubicaciones alternativas para las carpetas de instantáneas
  Las ubicaciones alternativas para las instantáneas permiten almacenar archivos de instantáneas en una ubicación distinta de la predeterminada o en otra ubicación además de la predeterminada, que suele encontrarse en el distribuidor. Las ubicaciones alternativas pueden encontrarse en otro servidor, en una unidad de red o en medios extraíbles, como discos CD-ROM o discos extraíbles.  
  
 Las ubicaciones alternativas de las instantáneas se almacenan como una propiedad de la publicación. Debido a que la ubicación alternativa de la instantánea es una propiedad de la publicación, el Agente de distribución y el de mezcla pueden localizar la instantánea adecuada como parte del proceso de sincronización.  
  
 Si desea especificar una ubicación diferente para la carpeta de instantáneas o si desea comprimir los archivos de instantáneas, cree la publicación sin crear la instantánea inicial inmediatamente, defina las propiedades de la publicación para la ubicación de la instantánea y ejecute el Agente de instantáneas para dicha publicación. Si cambia la ubicación alternativa después de crear la instantánea inicial, la ubicación de una instantánea generada para la publicación no se reubicará en la nueva ubicación alternativa. En este caso, dependiendo de la configuración de la publicación, es posible que el Agente de mezcla o el Agente de distribución encuentren los archivos de instantáneas en la nueva ubicación alternativa.  
  
> [!NOTE]  
>  No especifique una ubicación alternativa (con el cuadro de diálogo **Propiedades de la publicación** o [sp_changepublication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-changepublication-transact-sql)), que sea la misma que la ubicación de la carpeta predeterminada de instantáneas.  
  
> [!CAUTION]  
>  No use WebSync y las ubicaciones alternativas de carpeta de instantáneas a la vez.  
  
 **Para especificar ubicaciones alternativas de instantáneas**  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]: [Especificar una ubicación de carpeta de instantáneas alternativa](snapshot-options.md#snapshot-folder-locations) 
  
-   Programación de la replicación [!INCLUDE[tsql](../../includes/tsql-md.md)]: [Configurar propiedades de instantáneas &#40;programación de la replicación con Transact-SQL&#41;](publish/configure-snapshot-properties-replication-transact-sql-programming.md)  
  
## <a name="see-also"></a>Vea también  
 [Inicializar una suscripción con una instantánea](initialize-a-subscription-with-a-snapshot.md)   
 [Opciones de instantánea](snapshot-options.md)  
  
  
