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
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- database objects [SMO]
- objects [SMO]
ms.assetid: 702fd63d-8734-4a02-872e-aecfb037c787
caps.latest.revision: "33"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d9b2565474a777bbaddc6b659227a88bc1d2d609
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="creating-altering-and-removing-database-objects"></a>Crear, modificar y quitar objetos de base de datos
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]Las fases de la creación de objetos SMO son los siguientes:  
  
1.  Crear una instancia del objeto.  
  
2.  Establecer las propiedades del objeto.  
  
3.  Crear instancias de objetos secundarios.  
  
4.  Establecer las propiedades de los objetos secundarios.  
  
5.  Crear el objeto.  
  
 Cuando se crean instancias de objetos SMO en una aplicación SMO, no existen en la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] hasta que se emite el método **Crear** . Sin embargo, no es necesario emitir un método **Create** para cada objeto. Si un objeto tiene un conjunto de objetos secundarios, solo hace falta el objeto primario para ejecutar el método **Create** . Por ejemplo, la definición de una tabla requiere que contenga al menos una columna para existir. Asimismo, una columna no puede existir aislada sin una tabla. Hay una relación de codependencia entre la tabla y sus columnas.  
  
 El método <xref:Microsoft.SqlServer.Management.Dmf.Policy.Alter%2A> le permite hacer cambios en un objeto. Si se realizan varios cambios en un objeto, como agregar objetos secundarios a una de las colecciones del objeto o cambiar un valor de propiedad, se agrupan por lotes y se ejecutan como uno solo. El método **Alter** reduce el tráfico de red y mejora el rendimiento general.  
  
 La instrucción **Drop** se utiliza para quitar un objeto y todos los objetos secundarios codependientes que hicieron falta para crear el objeto inicialmente.  
  
## <a name="see-also"></a>Vea también  
 [Modelo de objetos de SMO](../../../relational-databases/server-management-objects-smo/smo-object-model.md)  
  
  
