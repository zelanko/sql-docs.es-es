---
title: "RDS devuelve &quot;objeto Stream no leído&quot; Error | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- stream not read error in RDS [ADO]
ms.assetid: cb5a68f8-dba4-41da-bafd-04efe53706b7
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b5c0cbc0d8c83a2d36fc931616046b0261938a0a
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="rds-returns-quotstream-not-readquot-error"></a>RDS devuelve &quot;objeto Stream no leído&quot; Error
"El objeto de secuencia no se pudo leer porque está vacío o la posición actual está al final de la secuencia. Para las secuencias no está vacío, establezca la posición actual con la propiedad de posición. Para determinar si una secuencia está vacía, compruebe la propiedad Size."  
  
 Si ve este mensaje de error, puede ha intentado utilizar una consulta jerárquica parametrizada a través de http. RDS no le permiten usar remota jerarquías parametrizadas.  
  
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, componentes de servidor RDS ya no están incluidos en el sistema operativo Windows (consulte Windows 8 y [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obtener más detalles). Componentes de cliente RDS se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Las aplicaciones que utilizan RDS deben migrar a [servicio de datos de WCF](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="see-also"></a>Vea también  
 [Conceptos básicos de RDS](../../../ado/guide/remote-data-service/rds-fundamentals.md)



