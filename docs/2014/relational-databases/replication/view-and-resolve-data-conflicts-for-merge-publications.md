---
title: Ver y resolver conflictos de datos para publicaciones de mezcla (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- merge replication conflict resolution [SQL Server replication], viewing conflicts
- viewing conflict information
- conflict resolution [SQL Server replication], merge replication
ms.assetid: aeee9546-4480-49f9-8b1e-c71da1f056c7
caps.latest.revision: 40
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 95df6108930543ce728b76c304578aab21927fde
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37209025"
---
# <a name="view-and-resolve-data-conflicts-for-merge-publications-sql-server-management-studio"></a>Ver y resolver conflictos de datos para publicaciones de mezcla (SQL Server Management Studio)
  Los conflictos en la replicación de mezcla se solucionan con el solucionador especificado para cada artículo. De manera predeterminada, los conflictos se resuelven sin necesidad de intervención del usuario. No obstante, es posible ver los conflictos y modificar el resultado de la resolución en el Visor de conflictos de replicación de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 Los datos de conflictos están disponibles en el Visor de conflictos de replicación durante el tiempo especificado como período de retención de conflictos (con un valor predeterminado de 14 días). Para configurar el período de retención de conflictos:  
  
-   Especifique un valor de retención para el parámetro **@conflict_retention** de [sp_addmergepublication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql).  
  
-   Especifique un valor de **conflict_retention** para el parámetro **@property** y un valor de retención para el parámetro **@value** de [sp_changemergepublication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql).  
  
 De manera predeterminada, la información del conflicto se almacena:  
  
-   En el publicador y en el suscriptor, si el nivel de compatibilidad de la publicación es igual o superior a 90RTM.  
  
-   En el publicador, si el nivel de compatibilidad de la publicación es inferior a 80RTM.  
  
-   En el publicador, si los suscriptores utilizan [!INCLUDE[ssEW](../../includes/ssew-md.md)]. No se pueden almacenar datos en conflicto en los suscriptores de [!INCLUDE[ssEW](../../includes/ssew-md.md)] .  
  
 La propiedad **conflict_logging** de la publicación controla el almacenamiento de la información del conflicto. Para más información, vea [sp_addmergepublication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql) y [sp_changemergepublication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql).  
  
 Los conflictos también se pueden solucionar de forma interactiva durante la sincronización, con el Solucionador interactivo de [!INCLUDE[msCoName](../../includes/msconame-md.md)] . El Solucionador interactivo está disponible a través del Administrador de sincronización de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows. Para más información, vea [Sincronizar una suscripción mediante el Administrador de sincronización de Windows (Administrador de sincronización de Windows)](synchronize-a-subscription-using-windows-synchronization-manager.md).  
  
### <a name="to-view-and-resolve-conflicts-for-merge-publications"></a>Para ver y solucionar conflictos de publicaciones de combinación  
  
1.  Conéctese al publicador (o al suscriptor, si procede) en [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]y expanda el nodo de servidor.  
  
2.  Expanda la carpeta **Replicación** y, a continuación, expanda la carpeta **Publicaciones locales** .  
  
3.  Haga clic con el botón secundario en la publicación para la que desea ver los conflictos y, a continuación, haga clic en **Ver conflictos**.  
  
    > [!NOTE]  
    >  Si especificó el valor **'subscriber'** para la propiedad **conflict_logging** , la opción de menú **Ver conflictos** no está disponible. Para ver los conflictos, inicie ConflictViewer.exe desde el símbolo del sistema. De forma predeterminada, ConflictViewer.exe se encuentra en el siguiente directorio: Microsoft SQL Server\100\Tools\Binn\VSShell\Common7\IDE. Para obtener una lista de parámetros de inicio válidos, ejecute ConflictViewer.exe -?.  
  
4.  En el cuadro de diálogo **Seleccionar tabla de conflictos** , seleccione una base de datos, una publicación y una tabla para ver los conflictos correspondientes.  
  
5.  En el Visor de conflictos de replicación, puede:  
  
    -   Filtrar filas con los botones que aparecen a la derecha de la cuadrícula superior.  
  
    -   Seleccionar una fila en la cuadrícula superior para ver la información de esa fila en la cuadrícula inferior.  
  
    -   Seleccionar una o más filas en la cuadrícula superior y hacer clic en **Quitar**, lo que equivale a hacer clic en el botón **Enviar ganador** (sin realizar cambios en los datos).  
  
    -   Hacer clic en el botón de propiedades (**…**) para ver más información acerca de la columna involucrada en el conflicto.  
  
    -   Editar datos en la columna **Ganador del conflicto** o **Perdedor del conflicto** antes de enviar los datos (los datos son de solo lectura si la columna está en color gris).  
  
    -   Hacer clic en **Enviar ganador** para aceptar la fila designada como ganador del conflicto.  
  
    -   Hacer clic en **Enviar perdedor** para anular la resolución y propagar el valor designado como perdedor del conflicto a todos los nodos de la topología.  
  
    -   Seleccionar **Registrar los detalles de este conflicto** para registrar los datos del conflicto en un archivo. Para especificar la ubicación del archivo, elija el menú **Ver** y haga clic en **Opciones**. Escriba un valor o haga clic en el botón Examinar (**...**) y navegue al archivo apropiado. Haga clic en **Aceptar** para salir del cuadro de diálogo **Opciones** .  
  
6.  Cierre el Visor de conflictos de replicación.  
  
## <a name="see-also"></a>Vea también  
 [Advanced Merge Replication Conflict Detection and Resolution](merge/advanced-merge-replication-conflict-detection-and-resolution.md)   
 [Especificar un solucionador de artículos de mezcla](publish/specify-a-merge-article-resolver.md)  
  
  
