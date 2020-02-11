---
title: Enviar conjuntos de resultados al servidor (API de procedimiento almacenado extendido) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- extended stored procedures [SQL Server], sending result sets
- result sets [SQL Server], extended stored procedures
ms.assetid: 9d54673d-ea9d-4ac6-825a-f216ad8b0e34
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: a58c8eca585bbbe2c935c524840bc465992d45c5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "62511850"
---
# <a name="sending-result-sets-to-the-server-extended-stored-procedure-api"></a>Enviar conjuntos de resultados al servidor (API de procedimiento almacenado extendido)
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]En su lugar, use la integración con CLR.  
  
 Al enviar un conjunto de resultados [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]a, el procedimiento almacenado extendido debe llamar a la API adecuada de la siguiente manera:  
  
-   Se puede llamar a la función **srv_sendmsg** en cualquier orden antes o después de que todas las filas (si las hubiera) se hayan enviado con **srv_sendrow**. Todos los mensajes se deben enviar al cliente antes de que el estado de finalización se envíe con **srv_senddone**.  
  
-   Se llama a la función **srv_sendrow** una vez por cada fila enviada al cliente. Todas las filas se deben enviar al cliente antes de enviar cualquier mensaje, valor de estado o estado de finalización con **srv_sendmsg**, el argumento de **srv_status** de **srv_pfield**o **srv_senddone**.  
  
-   El envío de una fila en la que no se han definido todas sus columnas con **srv_describe** hace que la aplicación genere un mensaje de error informativo y devuelva FAIL al cliente. En este caso, la fila no se envía.  
  
## <a name="see-also"></a>Consulte también  
 [Crear procedimientos almacenados extendidos](creating-extended-stored-procedures.md)  
  
  
