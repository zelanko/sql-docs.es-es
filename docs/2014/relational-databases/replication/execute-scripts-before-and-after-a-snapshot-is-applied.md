---
title: Ejecutar Scripts antes y después de aplicar una instantánea (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- replication
ms.topic: conceptual
helpviewer_keywords:
- snapshots [SQL Server replication], scripts
- scripts [SQL Server replication], snapshots
- snapshot replication [SQL Server], scripts
ms.assetid: b7bb1e4c-5b48-4bb1-9dc8-47c911f2cc82
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b5fdb23fc81a4025ded4bf02a56df06014d4ca3d
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48155955"
---
# <a name="execute-scripts-before-and-after-a-snapshot-is-applied-sql-server-management-studio"></a>Ejecutar scripts antes y después de aplicar una instantánea (SQL Server Management Studio)
  Especifique un script opcional para que se ejecute antes o después de aplicar la instantánea en la página **Instantánea** del cuadro de diálogo **Propiedades de la publicación: \<Publicación>**. Para obtener más información sobre el acceso a este cuadro de diálogo, vea [View and Modify Publication Properties](publish/view-and-modify-publication-properties.md).  
  
> [!NOTE]  
>  Estas opciones no están disponibles si la opción **Formato de instantánea** se establece en **Carácter**.  
  
### <a name="to-execute-a-script-before-or-after-a-snapshot-is-applied"></a>Para ejecutar un script antes o después de aplicar una instantánea  
  
1.  En la página **Instantánea** del cuadro de diálogo **Propiedades de la publicación: \<Publicación>**:  
  
    -   Para especificar un script para que se ejecute antes de aplicar la instantánea, haga clic en **Examinar** para navegar al script, o escriba la ruta de acceso del script en el cuadro de texto **Antes de aplicar la instantánea, ejecutar este script** .  
  
        > [!NOTE]  
        >  El Agente de distribución o el Agente de mezcla debe tener permisos de lectura para el directorio especificado. Si utiliza suscripciones de extracción, debe especificar un directorio compartido como ruta de acceso de convención de nomenclatura universal (UNC), por ejemplo \\\nombreDeEquipo\scripts\myscript.sql.  
  
    -   Para especificar un script para que se ejecute después de aplicar la instantánea, haga clic en **Examinar** para navegar al script, o escriba la ruta de acceso UNC al script en el cuadro de texto **Después de aplicar la instantánea, ejecutar este script** .  
  
2.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Vea también  
 [Configurar propiedades de instantáneas &#40;programación de la replicación con Transact-SQL&#41;](publish/configure-snapshot-properties-replication-transact-sql-programming.md)   
 [Cambiar las propiedades de la publicación y de los artículos](publish/change-publication-and-article-properties.md)   
 [Ejecutar scripts antes y después de aplicar la instantánea](execute-scripts-before-and-after-the-snapshot-is-applied.md)   
 [Inicializar una suscripción con una instantánea](initialize-a-subscription-with-a-snapshot.md)  
  
  
