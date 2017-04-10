---
title: "Ver y resolver conflictos de datos para publicaciones de mezcla (SQL Server Management Studio) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "resolución de conflictos de replicación de mezcla [replicación de SQL Server], ver conflictos"
  - "ver información de conflictos"
  - "resolución de conflictos [replicación de SQL Server], replicación de mezcla"
ms.assetid: aeee9546-4480-49f9-8b1e-c71da1f056c7
caps.latest.revision: 41
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# Ver y resolver conflictos de datos para publicaciones de mezcla (SQL Server Management Studio)
  Los conflictos en la replicación de mezcla se solucionan con el solucionador especificado para cada artículo. De manera predeterminada, los conflictos se resuelven sin necesidad de intervención del usuario. No obstante, es posible ver los conflictos y modificar el resultado de la resolución en el Visor de conflictos de replicación de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 Los datos de conflictos están disponibles en el Visor de conflictos de replicación durante el tiempo especificado como período de retención de conflictos (con un valor predeterminado de 14 días). Para configurar el período de retención de conflictos:  
  
-   Especifique un valor de retención para la **@conflict_retention** parámetro de [sp_addmergepublication & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md).  
  
-   Especifique un valor de **conflict_retention** para el **@property** parámetro y una retención de valor para el **@value** parámetro de [sp_changemergepublication & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md).  
  
 De manera predeterminada, la información del conflicto se almacena:  
  
-   En el publicador y en el suscriptor, si el nivel de compatibilidad de la publicación es igual o superior a 90RTM.  
  
-   En el publicador, si el nivel de compatibilidad de la publicación es inferior a 80RTM.  
  
-   En el publicador, si los suscriptores utilizan [!INCLUDE[ssEW](../../includes/ssew-md.md)]. No se pueden almacenar datos en conflicto en los suscriptores de [!INCLUDE[ssEW](../../includes/ssew-md.md)] .  
  
 Almacenamiento de información de conflictos se controla mediante la **conflict_logging** propiedad de publicación. Para obtener más información, consulte [sp_addmergepublication & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md) y [sp_changemergepublication & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md).  
  
 Los conflictos también se pueden solucionar de forma interactiva durante la sincronización, con el Solucionador interactivo de [!INCLUDE[msCoName](../../includes/msconame-md.md)] . El Solucionador interactivo está disponible a través del Administrador de sincronización de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows. Para obtener más información, consulte [sincronizar una suscripción utilizando Windows Synchronization Manager & #40; Administrador de sincronización de Windows & #41;](../../relational-databases/replication/synchronize a subscription using windows synchronization manager.md).  
  
### Para ver y solucionar conflictos de publicaciones de combinación  
  
1.  Conectar con el publicador (o el suscriptor, si procede) en [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], y, a continuación, expanda el nodo del servidor.  
  
2.  Expanda la carpeta **Replicación** y, a continuación, expanda la carpeta **Publicaciones locales** .  
  
3.  Haga clic en la publicación para el que desea ver los conflictos y, a continuación, haga clic en **Ver conflictos de**.  
  
    > [!NOTE]  
    >  Si especifica un valor de **'subscriber'** para el **conflict_logging** propiedad, la **Ver conflictos** no está disponible la opción de menú. Para ver los conflictos, inicie ConflictViewer.exe desde el símbolo del sistema. De forma predeterminada, ConflictViewer.exe se encuentra en el siguiente directorio: Microsoft SQL Server\100\Tools\Binn\VSShell\Common7\IDE. Para obtener una lista de parámetros de inicio válidos, ejecute ConflictViewer.exe -?.  
  
4.  En el cuadro de diálogo **Seleccionar tabla de conflictos** , seleccione una base de datos, una publicación y una tabla para ver los conflictos correspondientes.  
  
5.  En el Visor de conflictos de replicación, puede:  
  
    -   Filtrar filas con los botones que aparecen a la derecha de la cuadrícula superior.  
  
    -   Seleccionar una fila en la cuadrícula superior para ver la información de esa fila en la cuadrícula inferior.  
  
    -   Seleccione una o más filas en la cuadrícula superior y, a continuación, haga clic en **quitar**, que es equivalente a hacer clic en el **Enviar ganador** botón (sin realizar cambios en los datos).  
  
    -   Haga clic en el botón de propiedades (**...**) ver más información sobre una columna involucrado en un conflicto.  
  
    -   Modificar datos en el **ganador del conflicto** o **perdedor del conflicto** columna antes de enviar los datos (datos están de sólo lectura si la columna es de color gris).  
  
    -   Hacer clic en **Enviar ganador** para aceptar la fila designada como ganador del conflicto.  
  
    -   Hacer clic en **Enviar perdedor** para anular la resolución y propagar el valor designado como perdedor del conflicto a todos los nodos de la topología.  
  
    -   Seleccionar **Registrar los detalles de este conflicto** para registrar los datos del conflicto en un archivo. Para especificar la ubicación del archivo, elija el menú **Ver** y haga clic en **Opciones**. Escriba un valor o haga clic en el botón Examinar (**...**) y, a continuación, navegue hasta el archivo apropiado. Haga clic en **Aceptar** para salir del cuadro de diálogo **Opciones** .  
  
6.  Cierre el Visor de conflictos de replicación.  
  
## Vea también  
 [Detección y resolución de conflictos de replicación de mezcla avanzada](../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)   
 [Especificar un solucionador de artículos de mezcla](../../relational-databases/replication/publish/specify-a-merge-article-resolver.md)  
  
  