---
description: Enviar conjuntos de resultados al servidor (API de procedimiento almacenado extendido)
title: Enviar conjuntos de resultados al servidor (API de procedimiento almacenado extendido)
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- extended stored procedures [SQL Server], sending result sets
- result sets [SQL Server], extended stored procedures
ms.assetid: 9d54673d-ea9d-4ac6-825a-f216ad8b0e34
author: rothja
ms.author: jroth
ms.custom: seo-dt-2019
ms.openlocfilehash: 4747c464956d4c1da804a4bf9182cbb507a45989
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88383141"
---
# <a name="sending-result-sets-to-the-server-extended-stored-procedure-api"></a>Enviar conjuntos de resultados al servidor (API de procedimiento almacenado extendido)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] En su lugar, utilice la integración con CLR.  
  
 Al enviar un conjunto de resultados a [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , el procedimiento almacenado extendido debe llamar a la API adecuada de la siguiente manera:  
  
-   Se puede llamar a la función **srv_sendmsg** en cualquier orden antes o después de que todas las filas (si las hubiera) se hayan enviado con **srv_sendrow**. Todos los mensajes se deben enviar al cliente antes de que el estado de finalización se envíe con **srv_senddone**.  
  
-   Se llama a la función **srv_sendrow** una vez por cada fila enviada al cliente. Todas las filas se deben enviar al cliente antes de enviar cualquier mensaje, valor de estado o estado de finalización con **srv_sendmsg**, el argumento de **srv_status** de **srv_pfield**o **srv_senddone**.  
  
-   El envío de una fila en la que no se han definido todas sus columnas con **srv_describe** hace que la aplicación genere un mensaje de error informativo y devuelva FAIL al cliente. En este caso, la fila no se envía.  
  
## <a name="see-also"></a>Consulte también  
 [Crear procedimientos almacenados extendidos](../../relational-databases/extended-stored-procedures-programming/creating-extended-stored-procedures.md)  
  
  
