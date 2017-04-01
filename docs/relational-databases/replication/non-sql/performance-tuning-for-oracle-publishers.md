---
title: "Optimizar el rendimiento de publicadores de Oracle | Microsoft Docs"
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
  - "publicación de Oracle [replicación de SQL Server], optimización del rendimiento"
ms.assetid: 32c0b4ec-c166-45a3-b41e-38a30fd56813
caps.latest.revision: 34
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 34
---
# Optimizar el rendimiento de publicadores de Oracle
  Arquitectura de publicación es similar a Oracle la [!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] arquitectura de publicación, por tanto, el primer paso en la optimización de la replicación de Oracle para el rendimiento requiere seguir las recomendaciones de optimización generales se encuentra en [mejorar el rendimiento de la replicación General](../../../relational-databases/replication/administration/enhance-general-replication-performance.md).  
  
 Además, existen dos opciones para publicadores de Oracle que están relacionadas con el rendimiento:  
  
-   Especificar la opción de publicación adecuada: Oracle o Puerta de enlace de Oracle.  
  
-   Configurar el trabajo del conjunto de transacciones para procesar cambios en el publicador en un intervalo adecuado.  
  
## Especificar la opción de publicación adecuada  
 La opción de puerta de enlace de Oracle proporciona mejor rendimiento que la opción Completo. No obstante, esta opción no se puede utilizar para publicar la misma tabla en varias publicaciones transaccionales. Una tabla puede aparecer como máximo en una publicación transaccional y en cualquier número de publicaciones de instantánea. Si necesita publicar la misma tabla en varias publicaciones transaccionales, elija la opción Completo de Oracle. Especifique esta opción al identificar el publicador de Oracle en el distribuidor de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Para más información, consulte [Create a Publication from an Oracle Database](../../../relational-databases/replication/publish/create-a-publication-from-an-oracle-database.md).  
  
## Configurar el trabajo del conjunto de transacciones  
 Los cambios en tablas de Oracle publicadas se procesan en grupos denominados conjuntos de transacciones. Para garantizar la coherencia transaccional, cada conjunto de transacciones se confirma como una sola transacción en la base de datos de distribución. Si el conjunto de transacciones se hace demasiado grande, no se puede procesar eficazmente como una sola transacción.  
  
 De forma predeterminada, los conjuntos de transacciones se crean solo con el Agente de registro del LOG. Si, durante períodos de gran actividad de cambios, el Agente de registro del LOG no se ejecuta o no puede conectar desde el distribuidor de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] al publicador de Oracle, los conjuntos de transacciones pueden hacerse incontrolablemente grandes. Para prevenir este problema, asegúrese de que los conjuntos de transacciones se crean a intervalos regulares, incluso si el Agente de registro del LOG no se ejecuta o no puede conectar al publicador de Oracle.  
  
 Los conjuntos de transacciones se pueden crear con el trabajo Xactset (un trabajo de base de datos de Oracle instalado por la replicación), que utiliza el mismo mecanismo que el Agente de registro del LOG para crear conjuntos. Cada vez que se ejecuta el trabajo, se crea un nuevo conjunto de transacciones. La próxima vez que se ejecuta el Agente de registro del LOG, el agente procesa los conjuntos que se han creado. Si aún existen cambios pendientes después de haber procesado todos los conjuntos de transacciones existentes, el Agente de registro del LOG crea y procesa uno o varios conjuntos de transacciones adicionales.  
  
 Para configurar el trabajo del conjunto de transacciones, consulte [Configurar el trabajo de conjunto de transacciones para un publicador de Oracle & #40; Programación de Transact-SQL de replicación & #41;](../../../relational-databases/replication/administration/configure the transaction set job for an oracle publisher.md).  
  
## Vea también  
 [Configurar un publicador de Oracle](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md)   
 [Información general de la publicación de Oracle](../../../relational-databases/replication/non-sql/oracle-publishing-overview.md)  
  
  