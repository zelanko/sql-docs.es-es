---
title: Trabajar con objetos de base de datos | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: smo
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- database objects [SMO]
- objects [SMO]
ms.assetid: 702fd63d-8734-4a02-872e-aecfb037c787
caps.latest.revision: "33"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 556403a013ee348e836c059ef9b246b4d5606a87
ms.sourcegitcommit: cb2f9d4db45bef37c04064a9493ac2c1d60f2c22
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/12/2018
---
# <a name="creating-altering-and-removing-database-objects"></a>Crear, modificar y quitar objetos de base de datos
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  Éstas son las fases de la creación de objetos SMO:  
  
1.  Crear una instancia del objeto.  
  
2.  Establecer las propiedades del objeto.  
  
3.  Crear instancias de objetos secundarios.  
  
4.  Establecer las propiedades de los objetos secundarios.  
  
5.  Crear el objeto.  
  
 Cuando se crean instancias de objetos SMO en una aplicación SMO, no existen en la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] hasta que se emite el método **Crear** . Sin embargo, no es necesario emitir un método **Create** para cada objeto. Si un objeto tiene un conjunto de objetos secundarios, solo hace falta el objeto primario para ejecutar el método **Create** . Por ejemplo, la definición de una tabla requiere que contenga al menos una columna para existir. Asimismo, una columna no puede existir aislada sin una tabla. Hay una relación de codependencia entre la tabla y sus columnas.  
  
 El método <xref:Microsoft.SqlServer.Management.Dmf.Policy.Alter%2A> le permite hacer cambios en un objeto. Si se realizan varios cambios en un objeto, como agregar objetos secundarios a una de las colecciones del objeto o cambiar un valor de propiedad, se agrupan por lotes y se ejecutan como uno solo. El método **Alter** reduce el tráfico de red y mejora el rendimiento general.  
  
 La instrucción **Drop** se utiliza para quitar un objeto y todos los objetos secundarios codependientes que hicieron falta para crear el objeto inicialmente.  
  
## <a name="see-also"></a>Vea también  
 [Modelo de objetos SMO](../../../relational-databases/server-management-objects-smo/smo-object-model.md)  
  
  
