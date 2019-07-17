---
title: Acceso al contexto de consulta en procedimientos almacenados | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: olap
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 1679b5ddaf2c3abefb6da4e89e97e84193593630
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "68209398"
---
# <a name="accessing-query-context-in-stored-procedures"></a>Acceder al contexto de la consulta en los procedimientos almacenados
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  El contexto de ejecución de un procedimiento almacenado está disponible en el código del procedimiento almacenado como el **contexto** objeto del modelo de objetos de servidor ADOMD.NET. Éste es un contexto de solo lectura y no puede ser modificado por el procedimiento almacenado. Las propiedades siguientes están disponibles en este objeto.  
  
|Property|Escriba|Descripción|  
|--------------|----------|-----------------|  
|**CurrentCube**|Cube|El cubo del contexto de consulta actual.|  
|**CurrentDatabaseName**|Cadena|El identificador de la base de datos actual.|  
|**CurrentConnection**|Conexión|Una referencia al objeto de conexión en el contexto actual.|  
|**Pasar**|Entero|Número de paso del contexto actual.|  
  
 El **contexto** existe un objeto cuando se usa el modelo de objetos de expresiones multidimensionales (MDX) en un procedimiento almacenado. No está disponible cuando el modelo del objeto MDX se usa en un cliente. El **contexto** objeto explícitamente no es pasar o devolver el procedimiento almacenado. Se encuentra disponible durante la ejecución del procedimiento almacenado.  
  
## <a name="see-also"></a>Vea también  
 [Administración de los ensamblados de modelos multidimensionales](../../analysis-services/multidimensional-models/multidimensional-model-assemblies-management.md)   
 [Definición de procedimientos almacenados](../../analysis-services/multidimensional-models-extending-olap-stored-procedures/defining-stored-procedures.md)  
  
  
