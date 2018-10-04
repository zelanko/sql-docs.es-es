---
title: Enviar conjuntos de resultados en el servidor (API de procedimiento almacenado extendido) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- extended stored procedures [SQL Server], sending result sets
- result sets [SQL Server], extended stored procedures
ms.assetid: 9d54673d-ea9d-4ac6-825a-f216ad8b0e34
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 9766b73f624362a24c4b9e91ccd279cbcaabc527
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48137895"
---
# <a name="sending-result-sets-to-the-server-extended-stored-procedure-api"></a>Enviar conjuntos de resultados al servidor (API de procedimiento almacenado extendido)
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] En su lugar, utilice la integración con CLR.  
  
 Al enviar un conjunto de resultados a [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], el procedimiento almacenado extendido debe llamar a la API adecuada como sigue:  
  
-   El **srv_sendmsg** función se puede llamar en cualquier orden antes o después de han enviado todas las filas (si existe) con **srv_sendrow**. Todos los mensajes se deben enviar al cliente antes de enviar el estado de finalización con **srv_senddone**.  
  
-   Se llama a la función **srv_sendrow** una vez por cada fila enviada al cliente. Todas las filas se deben enviar al cliente antes de cualquier mensaje, el valor de estado o estado de finalización se envía con **srv_sendmsg**, **srv_status** argumento de **srv_pfield**, o **srv_senddone**.  
  
-   Envío de una fila que no se ha definido con todas sus columnas **srv_describe** hace que la aplicación provoque un mensaje de error informativo y devuelva FAIL al cliente. En este caso, la fila no se envía.  
  
## <a name="see-also"></a>Vea también  
 [Crear procedimientos almacenados extendidos](creating-extended-stored-procedures.md)  
  
  
