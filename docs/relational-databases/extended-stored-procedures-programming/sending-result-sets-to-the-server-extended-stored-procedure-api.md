---
title: Enviar conjuntos de resultados en el servidor (API de procedimiento almacenado extendido) | Documentos de Microsoft
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: extended-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- extended stored procedures [SQL Server], sending result sets
- result sets [SQL Server], extended stored procedures
ms.assetid: 9d54673d-ea9d-4ac6-825a-f216ad8b0e34
caps.latest.revision: 
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 897addc38cc2bbff5ccd536692750a3d0c75cd7b
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/09/2018
---
# <a name="sending-result-sets-to-the-server-extended-stored-procedure-api"></a>Enviar conjuntos de resultados al servidor (API de procedimiento almacenado extendido)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] En su lugar, use la integración con CLR.  
  
 Al enviar un conjunto de resultados a [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], el procedimiento almacenado extendido debe llamar a la API adecuada como sigue:  
  
-   El **srv_sendmsg** función se puede llamar en cualquier orden antes o después de han enviado todas las filas (si existe) con **srv_sendrow**. Todos los mensajes se deben enviar al cliente antes de enviar el estado de finalización con **srv_senddone**.  
  
-   Se llama a la función **srv_sendrow** una vez por cada fila enviada al cliente. Todas las filas se deben enviar al cliente antes de los mensajes, los valores de estado o estado de finalización se envía con **srv_sendmsg**, **srv_status** argumento de **srv_pfield**, o **srv_senddone**.  
  
-   Envío de una fila que no se ha definido con todas sus columnas **srv_describe** hace que la aplicación genera un mensaje de error informativo y devuelva FAIL al cliente. En este caso, la fila no se envía.  
  
## <a name="see-also"></a>Vea también  
 [Crear procedimientos almacenados extendidos](../../relational-databases/extended-stored-procedures-programming/creating-extended-stored-procedures.md)  
  
  
