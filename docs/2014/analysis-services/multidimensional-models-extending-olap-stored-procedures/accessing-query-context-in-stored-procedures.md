---
title: Acceso al contexto de consulta en procedimientos almacenados | Microsoft Docs
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
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 28aafacda2e9880a79201fd07ca41fb15959e87b
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37239845"
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
 [Administración de los ensamblados de modelos multidimensionales](../multidimensional-models/multidimensional-model-assemblies-management.md)   
 [Definición de procedimientos almacenados](../multidimensional-models-extending-olap-stored-procedures/defining-stored-procedures.md)  
  
  
