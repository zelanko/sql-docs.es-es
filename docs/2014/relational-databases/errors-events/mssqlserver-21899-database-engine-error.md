---
title: MSSQLSERVER_21899 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 21899 (Database Engine error)
ms.assetid: 32b87a7c-5380-4638-b147-dd78618f6625
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: d40ee92b98999cd6b88a469a02f290e68ca06559
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "62915023"
---
# <a name="mssqlserver_21899"></a>MSSQLSERVER_21899
    
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre de producto|SQL Server|  
|Id. de evento|21899|  
|Origen de eventos|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|SQLErrorNum21899|  
|Texto del mensaje|La consulta en el publicador redireccionado '%s' para determinar si hay entradas de sysserver para los suscriptores del publicador original '%s' no se ha realizado por el error '%d', mensaje de error '%s.|  
  
## <a name="explanation"></a>Explicación  
 
  `sp_validate_redirected_publisher` consulta las tablas de metadatos de suscripción de la base de datos del publicador en el servidor remoto para determinar los suscriptores asociados. Se devuelve el error 21899 si no se puede realizar esta consulta. La consulta de validación requiere acceso a la base de datos publicada en el publicador redirigido. Si el inicio de sesión especificado cuando se llama a `sp_adddistpublisher` para el publicador original no está autorizado para tener acceso a la base de datos publicada en el publicador redirigido, se devuelve el error 21899.  
  
## <a name="user-action"></a>Acción del usuario  
 Revise el mensaje de error citado para determinar la causa del error y llevar a cabo una acción correctora adecuada  
  
  
