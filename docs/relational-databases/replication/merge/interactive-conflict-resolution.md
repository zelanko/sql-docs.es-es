---
title: "Resoluci&#243;n interactiva de conflictos | Microsoft Docs"
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
  - "resolución interactiva de conflictos [replicación de SQL Server]"
  - "solucionador interactivo [replicación de SQL Server]"
  - "artículos [replicación de SQL Server], resolución de conflictos"
  - "resolución de conflictos [replicación de SQL Server], replicación de mezcla"
ms.assetid: 172c60c7-f605-4eb5-b185-54ae9e9d3c60
caps.latest.revision: 34
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# Resoluci&#243;n interactiva de conflictos
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] la replicación proporciona una resolución interactiva, que permite resolver conflictos manualmente durante la sincronización a petición en [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Administrador de sincronización de Windows. El Solucionador interactivo es una interfaz gráfica que se activa en tiempo de ejecución y muestra datos para cada fila en conflicto; ofrece opciones para ver y modificar los datos en conflicto y solucionar cada conflicto individualmente.  
  
 El Solucionador interactivo es similar al Visor de conflictos. Sin embargo, el Visor de conflictos muestra los resultados de los conflictos ya resueltos después de la sincronización de mezcla; el Solucionador interactivo muestra cada conflicto antes de la resolución, lo que permite determinar el resultado de cada conflicto durante la sincronización de mezcla. Debe haber una persona disponible para supervisar el Solucionador interactivo en el momento en que se produzca un conflicto.  
  
> [!NOTE]  
>  La Resolución interactiva requiere el Administrador de sincronización de Windows. Si se realiza una sincronización fuera del Administrador de sincronización de Windows (por ejemplo, una sincronización programada o una sincronización a petición en [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] o en el Monitor de replicación), los conflictos se resuelven automáticamente sin intervención del usuario, según la resolución especificada para el artículo. Los conflictos que implican registros lógicos no se muestran en el Solucionador interactivo. Para ver información acerca de estos conflictos, utilice procedimientos almacenados de replicación. Para obtener más información, consulte [Ver la información de conflictos para publicaciones de mezcla & #40; Programación de Transact-SQL de replicación & #41;](../../../relational-databases/replication/view conflict information for merge publications.md).  
  
## Solucionadores de artículos y el Solucionador interactivo  
 Los solucionadores de conflictos (ya sea el solucionador predeterminado, un controlador de lógica de negocios o un solucionador personalizado) se asignan a artículos específicos cuando se crea una publicación y utilizan un conjunto de reglas para determinar qué conjunto de datos debe utilizarse cuando se incluyen datos de filas en conflicto. El Solucionador interactivo no es un solucionador de conflictos independiente con reglas para determinar los ganadores y los perdedores de los conflictos, sino una herramienta que se utiliza junto con los solucionadores predeterminados y personalizados. El solucionador de artículos continúa determinando la fila ganadora y la perdedora, pero el Solucionador interactivo permite que intervenga el usuario para aceptar, rechazar o modificar los resultados.  
  
 Para utilizar el Solucionador interactivo, este debe estar habilitado para cada artículo y suscripción que lo necesite. Después de habilitarla para uno o varios artículos y suscripciones, el Solucionador interactivo se utiliza cuando se detectan conflictos durante la sincronización de mezcla.  
  
 Para utilizar la resolución interactiva, consulte [especificar la resolución interactiva de conflictos para artículos de mezcla](../../../relational-databases/replication/publish/specify-interactive-conflict-resolution-for-merge-articles.md) y [sincronizar una suscripción utilizando Windows Synchronization Manager & #40; Administrador de sincronización de Windows & #41;](../../../relational-databases/replication/synchronize a subscription using windows synchronization manager.md).  
  
## Vea también  
 [Detección y resolución de conflictos de replicación de mezcla avanzada](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)  
  
  