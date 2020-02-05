---
title: Visualización y resolución de conflictos de datos (combinación)
description: Obtenga información sobre cómo ver y solucionar conflictos de datos para publicaciones de combinación para SQL Server.
ms.custom: seo-lt-2019
ms.date: 11/20/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- merge replication conflict resolution [SQL Server replication], viewing conflicts
- viewing conflict information
- conflict resolution [SQL Server replication], merge replication
ms.assetid: aeee9546-4480-49f9-8b1e-c71da1f056c7
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 79dc4b26ee543aa99b9fc90e29f7bb6c7d571555
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "75321892"
---
# <a name="conflict-resolution-for-merge-replication"></a>Resolución de conflictos para la replicación de mezcla
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Los conflictos en la replicación de mezcla se solucionan con el solucionador especificado para cada artículo. De manera predeterminada, los conflictos se resuelven sin necesidad de intervención del usuario. No obstante, es posible ver los conflictos y modificar el resultado de la resolución en el Visor de conflictos de replicación de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 Los datos de conflictos están disponibles en el Visor de conflictos de replicación durante el tiempo especificado como período de retención de conflictos (con un valor predeterminado de 14 días). Para configurar el período de retención de conflictos:  
  
-   Especifique un valor de retención para el parámetro `@conflict_retention` de [sp_addmergepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md).  
  
-   Especifique un valor de **conflict_retention** para el parámetro `@property` y un valor de retención para el parámetro `@value` de [sp_changemergepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md).  
  
 De manera predeterminada, la información del conflicto se almacena:    
-   En el publicador y en el suscriptor, si el nivel de compatibilidad de la publicación es igual o superior a 90RTM.   
-   En el publicador, si el nivel de compatibilidad de la publicación es inferior a 80RTM.   
-   En el publicador, si los suscriptores utilizan [!INCLUDE[ssEW](../../includes/ssew-md.md)]. No se pueden almacenar datos en conflicto en los suscriptores de [!INCLUDE[ssEW](../../includes/ssew-md.md)] .  
  
 La propiedad **conflict_logging** de la publicación controla el almacenamiento de la información del conflicto. Para más información, vea [sp_addmergepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md) y [sp_changemergepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md).  
  
 Los conflictos también se pueden solucionar de forma interactiva durante la sincronización, con el Solucionador interactivo de [!INCLUDE[msCoName](../../includes/msconame-md.md)] . El Solucionador interactivo está disponible a través del Administrador de sincronización de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows. Para más información, vea [Sincronizar una suscripción mediante el Administrador de sincronización de Windows &#40;Administrador de sincronización de Windows&#41;](../../relational-databases/replication/synchronize-a-subscription-using-windows-synchronization-manager.md).  
  
## <a name="resolve-conflicts"></a>Resolución de conflictos  
  
1.  Conéctese al publicador (o al suscriptor, si procede) en [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] y expanda el nodo de servidor.  
  
2.  Expanda la carpeta **Replicación** y, a continuación, expanda la carpeta **Publicaciones locales** .  
  
3.  Haga clic con el botón secundario en la publicación para la que desea ver los conflictos y, a continuación, haga clic en **Ver conflictos**.  
  
    > [!NOTE]  
    >  Si especificó el valor **'subscriber'** para la propiedad **conflict_logging** , la opción de menú **Ver conflictos** no está disponible. Para ver los conflictos, inicie ConflictViewer.exe desde el símbolo del sistema. De forma predeterminada, ConflictViewer.exe se encuentra en el siguiente directorio: Microsoft SQL Server\100\Tools\Binn\VSShell\Common7\IDE. Para obtener una lista de parámetros de inicio válidos, ejecute ConflictViewer.exe -?.  
  
4.  En el cuadro de diálogo **Seleccionar tabla de conflictos** , seleccione una base de datos, una publicación y una tabla para ver los conflictos correspondientes.  
  
5.  En el Visor de conflictos de replicación, puede:  
  
    -   Filtrar filas con los botones que aparecen a la derecha de la cuadrícula superior.  
  
    -   Seleccionar una fila en la cuadrícula superior para ver la información de esa fila en la cuadrícula inferior.  
  
    -   Seleccionar una o más filas en la cuadrícula superior y hacer clic en **Quitar**, lo que equivale a hacer clic en el botón **Enviar ganador** (sin realizar cambios en los datos).  
  
    -   Hacer clic en el botón de propiedades ( **...** ) para ver más información sobre la columna involucrada en el conflicto.  
  
    -   Editar datos en la columna **Ganador del conflicto** o **Perdedor del conflicto** antes de enviar los datos (los datos son de solo lectura si la columna está en color gris).  
  
    -   Hacer clic en **Enviar ganador** para aceptar la fila designada como ganador del conflicto.  
  
    -   Hacer clic en **Enviar perdedor** para anular la resolución y propagar el valor designado como perdedor del conflicto a todos los nodos de la topología.  
  
    -   Seleccionar **Registrar los detalles de este conflicto** para registrar los datos del conflicto en un archivo. Para especificar la ubicación del archivo, elija el menú **Ver** y haga clic en **Opciones**. Escriba un valor o haga clic en el botón Examinar ( **...** ) y navegue al archivo apropiado. Haga clic en **Aceptar** para salir del cuadro de diálogo **Opciones** .  
  
6.  Cierre el Visor de conflictos de replicación.  

## <a name="view-conflict-information"></a>Visualización de la información de conflictos
Cuando se resuelve un conflicto en la replicación de mezcla, los datos de la fila que falta se escriben en una tabla de conflictos. Estos datos de conflicto se pueden ver mediante programación usando los procedimientos almacenados de replicación. Para más información, consulte [Replicación de mezcla avanzada: detección y resolución de conflictos](../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md).  
  
1.  En la base de datos de publicación del publicador, ejecute [sp_helpmergepublication](../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md). Tenga en cuenta los valores de las siguientes columnas en el conjunto de resultados:  
  
    -   **centralized_conflicts** : 1 indica que las filas de conflicto están almacenadas en el Publicador y 0 indica que las filas de conflicto no están almacenadas en el Publicador.  
  
    -   **decentralized_conflicts** : 1 indica que las filas de conflicto están almacenadas en el Suscriptor y 0 indica que las filas de conflicto no están almacenadas en el Suscriptor.  
  
        > [!NOTE]  
        >  El comportamiento del registro de conflictos de una publicación de combinación se establece mediante el parámetro `@conflict_logging` de [sp_addmergepublication](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md). El uso del parámetro `@centralized_conflicts` ha quedado en desuso.  
  
     En la tabla siguiente se describen los valores de estas columnas en función del valor especificado para `@conflict_logging`.  
  
    |Valor de @conflict_logging|centralized_conflicts|decentralized_conflicts|  
    |------------------------------|----------------------------|------------------------------|  
    |**publisher**|1|0|  
    |**suscriptor**|0|1|  
    |**ambos**|1|1|  
  
2.  En el publicador de la base de datos de publicación o en el suscriptor de la base de datos de suscripciones, ejecute [sp_helpmergearticleconflicts](../../relational-databases/system-stored-procedures/sp-helpmergearticleconflicts-transact-sql.md). Especifique un valor para `@publication` a fin de devolver únicamente información de conflicto para los artículos que pertenecen a una publicación concreta. Esto devuelve información de la tabla de conflictos para los artículos con conflictos. Tenga en cuenta el valor de **conflict_table** para cualquier artículo de interés. Si el valor de **conflict_table** para un artículo es NULL, basta con que elimine los conflictos que se han producido en este artículo.  
  
3.  (Opcional) Revise las filas de conflicto para los artículos de interés. Según los valores de **centralized_conflicts** y **decentralized_conflicts** del paso 1, realice una de las siguientes operaciones:  
  
    -   En la base de datos de publicación del publicador, ejecute [sp_helpmergeconflictrows](../../relational-databases/system-stored-procedures/sp-helpmergeconflictrows-transact-sql.md). Especifique una tabla de conflictos para el artículo (del paso 1) para `@conflict_table`. (Opcional) Especifique un valor de `@publication` para restringir la información de conflicto devuelta a una publicación concreta. Esto devuelve datos de fila y otra información para la fila perdedora.  
  
    -   En el suscriptor de la base de datos de suscripciones, ejecute [sp_helpmergeconflictrows](../../relational-databases/system-stored-procedures/sp-helpmergeconflictrows-transact-sql.md). Especifique una tabla de conflictos para el artículo (del paso 1) para `@conflict_table`. Esto devuelve datos de fila y otra información para la fila perdedora.  
  
## <a name="conflict-where-delete-failed"></a>Conflicto de error de eliminación   
  
1.  En la base de datos de publicación del publicador, ejecute [sp_helpmergepublication](../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md). Tenga en cuenta los valores de las siguientes columnas en el conjunto de resultados:  
  
    -   **centralized_conflicts** : 1 indica que las filas de conflicto están almacenadas en el Publicador y 0 indica que las filas de conflicto no están almacenadas en el Publicador.  
  
    -   **decentralized_conflicts** : 1 indica que las filas de conflicto están almacenadas en el Suscriptor y 0 indica que las filas de conflicto no están almacenadas en el Suscriptor.  
  
        > [!NOTE]  
        >  El comportamiento del registro de conflictos de una publicación de combinación se establece mediante el parámetro `@conflict_logging` de [sp_addmergepublication](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md). El uso del parámetro `@centralized_conflicts` ha quedado en desuso.  
  
2.  En el publicador de la base de datos de publicación o en el suscriptor de la base de datos de suscripciones, ejecute [sp_helpmergearticleconflicts](../../relational-databases/system-stored-procedures/sp-helpmergearticleconflicts-transact-sql.md). Especifique un valor para `@publication` a fin de devolver únicamente información de tabla de conflictos para los artículos que pertenecen a una publicación concreta. Esto devuelve información de la tabla de conflictos para los artículos con conflictos. Tenga en cuenta el valor de **source_object** para cualquier artículo de interés. Si el valor de **conflict_table** para un artículo es NULL, basta con que elimine los conflictos que se han producido en este artículo.  
  
3.  (Opcional) Revise la información de conflictos para conflictos de eliminación. Según los valores de **centralized_conflicts** y **decentralized_conflicts** del paso 1, realice una de las siguientes operaciones:  
  
    -   En la base de datos de publicación del publicador, ejecute [sp_helpmergedeleteconflictrows](../../relational-databases/system-stored-procedures/sp-helpmergedeleteconflictrows-transact-sql.md). Especifique el nombre de la tabla de origen (del paso 1) en la que el conflicto se ha producido para `@source_object`. (Opcional) Especifique un valor de `@publication` para restringir la información de conflicto devuelta a una publicación concreta. Esto devuelve elimine la información de eliminación de conflictos almacenada en el publicador.  
  
    -   En el suscriptor de la base de datos de suscripciones, ejecute [sp_helpmergedeleteconflictrows](../../relational-databases/system-stored-procedures/sp-helpmergedeleteconflictrows-transact-sql.md). Especifique el nombre de la tabla de origen (del paso 1) en la que el conflicto se ha producido para `@source_object`. (Opcional) Especifique un valor de `@publication` para restringir la información de conflicto devuelta a una publicación concreta. Esto devuelve elimine la información de eliminación de conflictos almacenada en el suscriptor.  
  
## <a name="see-also"></a>Consulte también  
 [Detección y resolución de conflictos de replicación de mezcla avanzada](../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)   
 [Especificar un solucionador de artículos de mezcla](../../relational-databases/replication/publish/specify-a-merge-article-resolver.md)  
  
  
