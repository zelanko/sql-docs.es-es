---
title: RDS devuelve &quot;un error de&quot; secuencia no leída | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- stream not read error in RDS [ADO]
ms.assetid: cb5a68f8-dba4-41da-bafd-04efe53706b7
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c89756e86a702217d5d9d8495bf62b0d27f52321
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "67922470"
---
# <a name="rds-returns-quotstream-not-readquot-error"></a>RDS devuelve &quot;un error de&quot; secuencia no leída
"No se pudo leer el objeto de secuencia porque está vacío o la posición actual está al final de la secuencia. En el caso de secuencias no vacías, establezca la posición actual con la propiedad Position. Para determinar si un flujo está vacío, Compruebe la propiedad size ".  
  
 Si ve este mensaje de error, es posible que haya intentado usar una consulta jerárquica parametrizada sobre http. RDS no permite el uso de jerarquías parametrizadas remotas.  
  
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, los componentes de servidor RDS ya no se incluyen en el sistema operativo Windows (consulte la guía de compatibilidad de Windows 8 y [Windows server 2012](https://www.microsoft.com/download/details.aspx?id=27416) para obtener más detalles). Los componentes de cliente RDS se quitarán en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Las aplicaciones que utilizan RDS deben migrar al [servicio de datos de WCF](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="see-also"></a>Consulte también  
 [Aspectos básicos de RDS](../../../ado/guide/remote-data-service/rds-fundamentals.md)


