---
title: RDS devuelve &quot;Stream no leída&quot; Error | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 65067452553f3a0c44259e12b294bc795baa9d12
ms.sourcegitcommit: 1a5448747ccb2e13e8f3d9f04012ba5ae04bb0a3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/12/2018
ms.locfileid: "51559962"
---
# <a name="rds-returns-quotstream-not-readquot-error"></a>RDS devuelve &quot;Stream no leída&quot; Error
"El objeto Stream no se puede leer porque está vacío o la posición actual está al final de la Stream. Para las secuencias de valores no vacíos, establezca la posición actual con la propiedad Position. Para determinar si un Stream está vacío, compruebe la propiedad de tamaño."  
  
 Si ve este mensaje de error, es posible que haya intentado utilizar una consulta parametrizada jerárquica a través de http. RDS no permite usar remotas jerarquías con parámetros.  
  
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, componentes de servidor RDS ya no están incluidos en el sistema operativo de Windows (consulte Windows 8 y [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obtener más detalles). Componentes de cliente RDS se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Deben migrar las aplicaciones que usan RDS a [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="see-also"></a>Vea también  
 [Aspectos básicos de RDS](../../../ado/guide/remote-data-service/rds-fundamentals.md)


