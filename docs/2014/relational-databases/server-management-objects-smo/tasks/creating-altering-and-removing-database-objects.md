---
title: Trabajar con objetos de base de datos | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- database objects [SMO]
- objects [SMO]
ms.assetid: 702fd63d-8734-4a02-872e-aecfb037c787
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d5190d6fcabe339d4d99e8b5001174c9f638b54a
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48148255"
---
# <a name="working-with-database-objects"></a>Trabajar con objetos de bases de datos
  Éstas son las fases de la creación de objetos SMO:  
  
1.  Crear una instancia del objeto.  
  
2.  Establecer las propiedades del objeto.  
  
3.  Crear instancias de objetos secundarios.  
  
4.  Establecer las propiedades de los objetos secundarios.  
  
5.  Crear el objeto.  
  
 Cuando se crean instancias de objetos SMO en una aplicación SMO, no existen en la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] hasta que se emite el método `Create`. Sin embargo, no es necesario emitir un método `Create` para cada objeto. Si un objeto tiene un conjunto de objetos secundarios, solo hace falta el objeto primario para ejecutar el método `Create`. Por ejemplo, la definición de una tabla requiere que contenga al menos una columna para existir. Asimismo, una columna no puede existir aislada sin una tabla. Hay una relación de codependencia entre la tabla y sus columnas.  
  
 El método <xref:Microsoft.SqlServer.Management.Dmf.Policy.Alter%2A> le permite hacer cambios en un objeto. Si se realizan varios cambios en un objeto, como agregar objetos secundarios a una de las colecciones del objeto o cambiar un valor de propiedad, se agrupan por lotes y se ejecutan como uno solo. El método `Alter` reduce el tráfico de red y mejora el rendimiento general.  
  
 La instrucción `Drop` se utiliza para quitar un objeto y todos los objetos secundarios codependientes que hicieron falta para crear el objeto inicialmente.  
  
## <a name="see-also"></a>Vea también  
 [Modelo de objetos de SMO](../smo-object-model.md)  
  
  
