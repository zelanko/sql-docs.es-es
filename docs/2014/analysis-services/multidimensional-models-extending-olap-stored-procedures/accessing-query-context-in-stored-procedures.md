---
title: Acceso al contexto de consulta en procedimientos almacenados | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- execution context [Analysis Services]
- stored procedures [Analysis Services], query context
- Context object
- query context [Analysis Services]
ms.assetid: bdc7dad8-2f22-4265-aba4-a3a451527840
caps.latest.revision: 22
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: ef60683eb410f0db5ba9e8d38ac227ca22dd9159
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36108696"
---
# <a name="accessing-query-context-in-stored-procedures"></a>Acceder al contexto de la consulta en los procedimientos almacenados
  El contexto de ejecución de un procedimiento almacenado se encuentra disponible dentro del código del procedimiento almacenado como el objeto `Context` del modelo de objeto del servidor ADOMD.NET. Éste es un contexto de solo lectura y no puede ser modificado por el procedimiento almacenado. Las propiedades siguientes están disponibles en este objeto.  
  
|Property|Tipo|Descripción|  
|--------------|----------|-----------------|  
|**CurrentCube**|Cube|El cubo del contexto de consulta actual.|  
|**CurrentDatabaseName**|String|El identificador de la base de datos actual.|  
|**CurrentConnection**|Conexión|Una referencia al objeto de conexión en el contexto actual.|  
|**Pasar**|Integer|Número de paso del contexto actual.|  
  
 El objeto `Context` existe cuando el modelo de objetos de expresiones multidimensionales (MDX) se usa en un procedimiento almacenado. No está disponible cuando el modelo del objeto MDX se usa en un cliente. El objeto `Context` no se pasa explícitamente al procedimiento almacenado, ni es devuelto por él. Se encuentra disponible durante la ejecución del procedimiento almacenado.  
  
## <a name="see-also"></a>Vea también  
 [Administración de ensamblados de modelos multidimensionales](../multidimensional-models/multidimensional-model-assemblies-management.md)   
 [Definición de procedimientos almacenados](../multidimensional-models-extending-olap-stored-procedures/defining-stored-procedures.md)  
  
  