---
title: Comando SET DELETED (Set DELETED Command) Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SET DELETED command [ODBC]
ms.assetid: 6b5e0086-156d-471d-8e7f-6c5fa9686cd5
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3b3302dc7eecca7135dab9dff5afa376169be0f1
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300885"
---
# <a name="set-deleted-command"></a>Comando de eliminaciones de Set
Especifica si se procesan los registros marcados para su eliminación y si están disponibles para su uso en otros comandos.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
SET DELETED ON | OFF  
```  
  
## <a name="arguments"></a>Argumentos  
 ACTIVAR  
 (Predeterminado para el controlador; el valor predeterminado para Visual FoxPro es OFF.) Especifica que los comandos que funcionan en registros (incluidos los registros de tablas relacionadas) mediante un ámbito omiten los registros marcados para su eliminación.  
  
 Apagado  
 Especifica que los comandos que funcionan en registros (incluidos los registros de tablas relacionadas) pueden tener acceso a los registros marcados para su eliminación mediante un ámbito.  
  
## <a name="remarks"></a>Observaciones  
 Las consultas que utilizan DELETED( ) para probar el estado de los registros se pueden optimizar con la tecnología Visual FoxPro Rushmore si la tabla está indexada en DELETED( ).  
  
> [!IMPORTANT]  
>  SET DELETED se omite si el ámbito predeterminado del comando es el registro actual o si incluye un ámbito de un único registro. INDEX siempre omite SET DELETED e indexa todos los registros de la tabla.  
  
## <a name="see-also"></a>Consulte también  
 [ELIMINAR, comando SQL](../../odbc/microsoft/delete-sql-command.md)
