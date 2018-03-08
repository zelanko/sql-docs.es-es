---
title: CHECKPOINT (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/27/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CHECKPOINT_TSQL
- CHECKPOINT
dev_langs:
- TSQL
helpviewer_keywords:
- events [SQL Server], checkpoints
- automatic checkpoints
- writing dirty pages to disk
- pages [SQL Server], dirty
- checkpoints [SQL Server]
- CHECKPOINT statement
- log truncate mode [SQL Server]
- dirty pages
- logs [SQL Server], checkpoints
- manual checkpoints [SQL Server]
- pages [SQL Server], checkpoints
ms.assetid: ccdfc689-ad4e-44c0-83f7-0f2cfcfb6406
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 6353bd534827ff9066bd7b184a09d67b5867c3cb
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/25/2018
---
# <a name="checkpoint-transact-sql"></a>CHECKPOINT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Genera un punto de comprobación manual en la base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a la que está conectado actualmente.  
  
> [!NOTE]  
>  Para obtener información sobre los diferentes tipos de puntos de comprobación de base de datos y la operación de punto de comprobación en general, vea [puntos de comprobación de base de datos &#40; SQL Server &#41; ](../../relational-databases/logs/database-checkpoints-sql-server.md).  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
CHECKPOINT [ checkpoint_duration ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *checkpoint_duration*  
 Especifica la cantidad de tiempo necesaria, en segundos, para que se complete el punto de comprobación manual. Cuando *checkpoint_duration* se especifica, el [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] intenta realizar el punto de control dentro de la duración solicitada. El *checkpoint_duration* debe ser una expresión de tipo **int** y debe ser mayor que cero. Cuando se omite este parámetro, el [!INCLUDE[ssDE](../../includes/ssde-md.md)] ajusta la duración del punto de comprobación para minimizar el impacto en el rendimiento de las aplicaciones de base de datos. *checkpoint_duration* es una opción avanzada.  
  
## <a name="factors-affecting-the-duration-of-checkpoint-operations"></a>Factores que afectan a la duración de las operaciones de puntos de comprobación  
 Generalmente, el tiempo necesario para una operación de punto de comprobación aumenta con el número de páginas desfasadas que la operación debe escribir. De forma predeterminada, para minimizar el impacto en el rendimiento de otras aplicaciones, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ajusta la frecuencia de escritura que una operación de punto de comprobación realiza. Reducir la frecuencia de escritura incrementa el tiempo que la operación de punto de comprobación necesita para completarse. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]usa esta estrategia para una instrucción checkpoint manual a menos que un *checkpoint_duration* se expresa en el comando CHECKPOINT.  
  
 El impacto de rendimiento de uso *checkpoint_duration* depende del número de páginas desfasadas, la actividad en el sistema y la duración real especificada. Por ejemplo, si el punto de control normalmente se completa en 120 segundos, especifica un *checkpoint_duration* de causas de 45 segundos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] destine más recursos al punto de control que asignaría de forma predeterminada. En cambio, especificar un *checkpoint_duration* de 180 segundos causaría [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para asignar menos recursos que podrían asignarse de forma predeterminada. En general, un valor bajo *checkpoint_duration* aumentará los recursos destinados al punto de comprobación, mientras que un valor elevado *checkpoint_duration* reducirá los recursos destinados al punto de control. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] siempre completa los puntos de comprobación si es posible, y la instrucción CHECKPOINT devuelve un valor inmediatamente cuando se completa un punto de comprobación. Por tanto, en algunos casos, un punto de comprobación puede llevar más o menos tiempo que la duración especificada.  
  
##  <a name="Security"></a> Seguridad  
  
### <a name="permissions"></a>Permissions  
 Permisos de punto de control de forma predeterminada a los miembros de la **sysadmin** rol fijo de servidor y el **db_owner** y **db_backupoperator** funciones fijas de base de datos y no son puede transferir.  
  
## <a name="see-also"></a>Vea también  
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [Puntos de comprobación de base de datos &#40;SQL Server&#41;](../../relational-databases/logs/database-checkpoints-sql-server.md)   
 [Configurar la opción de configuración del servidor de intervalo de recuperación](../../database-engine/configure-windows/configure-the-recovery-interval-server-configuration-option.md)   
 [SHUTDOWN &#40;Transact-SQL&#41;](../../t-sql/language-elements/shutdown-transact-sql.md)  
  
  
