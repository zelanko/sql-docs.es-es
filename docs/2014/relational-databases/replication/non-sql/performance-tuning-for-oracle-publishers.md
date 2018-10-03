---
title: Optimización del rendimiento de publicadores de Oracle | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- replication
ms.topic: conceptual
helpviewer_keywords:
- Oracle publishing [SQL Server replication], performance tuning
ms.assetid: 32c0b4ec-c166-45a3-b41e-38a30fd56813
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a73811a1a6d9c720e322d14031a004746198470b
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48124605"
---
# <a name="performance-tuning-for-oracle-publishers"></a>Optimizar el rendimiento de publicadores de Oracle
  La arquitectura de publicación de Oracle es similar a la arquitectura de publicación de [!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , por tanto el primer paso para optimizar la replicación de Oracle para un mejor rendimiento es seguir las recomendaciones generales de optimización que se encuentran en [Enhance General Replication Performance](../administration/enhance-general-replication-performance.md).  
  
 Además, existen dos opciones para publicadores de Oracle que están relacionadas con el rendimiento:  
  
-   Especificar la opción de publicación adecuada: Oracle o Puerta de enlace de Oracle.  
  
-   Configurar el trabajo del conjunto de transacciones para procesar cambios en el publicador en un intervalo adecuado.  
  
## <a name="specifying-the-appropriate-publishing-option"></a>Especificar la opción de publicación adecuada  
 La opción de puerta de enlace de Oracle proporciona mejor rendimiento que la opción Completo. No obstante, esta opción no se puede utilizar para publicar la misma tabla en varias publicaciones transaccionales. Una tabla puede aparecer como máximo en una publicación transaccional y en cualquier número de publicaciones de instantánea. Si necesita publicar la misma tabla en varias publicaciones transaccionales, elija la opción Completo de Oracle. Especifique esta opción al identificar el publicador de Oracle en el distribuidor de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Para más información, consulte [Create a Publication from an Oracle Database](../publish/create-a-publication-from-an-oracle-database.md).  
  
## <a name="configuring-the-transaction-set-job"></a>Configurar el trabajo del conjunto de transacciones  
 Los cambios en tablas de Oracle publicadas se procesan en grupos denominados conjuntos de transacciones. Para garantizar la coherencia transaccional, cada conjunto de transacciones se confirma como una sola transacción en la base de datos de distribución. Si el conjunto de transacciones se hace demasiado grande, no se puede procesar eficazmente como una sola transacción.  
  
 De forma predeterminada, los conjuntos de transacciones se crean solo con el Agente de registro del LOG. Si, durante períodos de gran actividad de cambios, el Agente de registro del LOG no se ejecuta o no puede conectar desde el distribuidor de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] al publicador de Oracle, los conjuntos de transacciones pueden hacerse incontrolablemente grandes. Para prevenir este problema, asegúrese de que los conjuntos de transacciones se crean a intervalos regulares, incluso si el Agente de registro del LOG no se ejecuta o no puede conectar al publicador de Oracle.  
  
 Los conjuntos de transacciones se pueden crear con el trabajo Xactset (un trabajo de base de datos de Oracle instalado por la replicación), que utiliza el mismo mecanismo que el Agente de registro del LOG para crear conjuntos. Cada vez que se ejecuta el trabajo, se crea un nuevo conjunto de transacciones. La próxima vez que se ejecuta el Agente de registro del LOG, el agente procesa los conjuntos que se han creado. Si aún existen cambios pendientes después de haber procesado todos los conjuntos de transacciones existentes, el Agente de registro del LOG crea y procesa uno o varios conjuntos de transacciones adicionales.  
  
 Para configurar el trabajo del conjunto de transacciones, consulte [Configuración del trabajo del conjunto de transacciones para un publicador de Oracle &#40;programa de la replicación con Transact-SQL&#41;](../administration/configure-the-transaction-set-job-for-an-oracle-publisher.md).  
  
## <a name="see-also"></a>Vea también  
 [Configurar un publicador de Oracle](configure-an-oracle-publisher.md)   
 [Información general de la publicación de Oracle](oracle-publishing-overview.md)  
  
  
