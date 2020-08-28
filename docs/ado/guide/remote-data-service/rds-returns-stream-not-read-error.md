---
description: RDS devuelve un &quot; error de secuencia no leída &quot;
title: RDS devuelve un &quot; error de secuencia no leída &quot; | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- stream not read error in RDS [ADO]
ms.assetid: cb5a68f8-dba4-41da-bafd-04efe53706b7
author: rothja
ms.author: jroth
ms.openlocfilehash: 23de3604b57f2b424a2166cc25f79bcb4ccbde09
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2020
ms.locfileid: "88977907"
---
# <a name="rds-returns-quotstream-not-readquot-error"></a>RDS devuelve un &quot; error de secuencia no leída &quot;
"No se pudo leer el objeto de secuencia porque está vacío o la posición actual está al final de la secuencia. En el caso de secuencias no vacías, establezca la posición actual con la propiedad Position. Para determinar si un flujo está vacío, Compruebe la propiedad size ".  
  
 Si ve este mensaje de error, es posible que haya intentado usar una consulta jerárquica parametrizada sobre http. RDS no permite el uso de jerarquías parametrizadas remotas.  
  
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, los componentes de servidor RDS ya no se incluyen en el sistema operativo Windows (consulte la guía de compatibilidad de Windows 8 y [Windows server 2012](https://www.microsoft.com/download/details.aspx?id=27416) para obtener más detalles). Los componentes de cliente RDS se quitarán en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Las aplicaciones que utilizan RDS deben migrar al [servicio de datos de WCF](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="see-also"></a>Consulte también  
 [Aspectos básicos de RDS](./rds-fundamentals.md)