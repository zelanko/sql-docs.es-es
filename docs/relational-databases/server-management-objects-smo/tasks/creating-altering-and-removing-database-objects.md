---
description: Crear, modificar y quitar objetos de base de datos
title: Trabajar con objetos de bases de datos
ms.custom: seo-dt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- database objects [SMO]
- objects [SMO]
ms.assetid: 702fd63d-8734-4a02-872e-aecfb037c787
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: f2ae7dbbfc762ed342ddc085afcb799f9b292966
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2020
ms.locfileid: "97468506"
---
# <a name="creating-altering-and-removing-database-objects"></a>Crear, modificar y quitar objetos de base de datos
[!INCLUDE [SQL Server ASDB, ASDBMI, ASDW ](../../../includes/applies-to-version/sql-asdb-asdbmi-asa.md)]

  Éstas son las fases de la creación de objetos SMO:  
  
1.  Crear una instancia del objeto.  
  
2.  Establecer las propiedades del objeto.  
  
3.  Crear instancias de objetos secundarios.  
  
4.  Establecer las propiedades de los objetos secundarios.  
  
5.  Crear el objeto.  

 Cuando se crean instancias de objetos SMO en una aplicación SMO, no existen en la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] hasta que se emite el método **Crear** . Sin embargo, no es necesario emitir un método **Create** para cada objeto. Si un objeto tiene un conjunto de objetos secundarios, solo hace falta el objeto primario para ejecutar el método **Create** . Por ejemplo, la definición de una tabla requiere que contenga al menos una columna para existir. Asimismo, una columna no puede existir aislada sin una tabla. Hay una relación de codependencia entre la tabla y sus columnas.  
  
 El método <xref:Microsoft.SqlServer.Management.Dmf.Policy.Alter%2A> le permite hacer cambios en un objeto. Si se realizan varios cambios en un objeto, como agregar objetos secundarios a una de las colecciones del objeto o cambiar un valor de propiedad, se agrupan por lotes y se ejecutan como uno solo. El método **Alter** reduce el tráfico de red y mejora el rendimiento general.  
  
 La instrucción **Drop** se utiliza para quitar un objeto y todos los objetos secundarios codependientes que hicieron falta para crear el objeto inicialmente.  
  
## <a name="see-also"></a>Consulte también  
 [Modelo de objetos SMO](../../../relational-databases/server-management-objects-smo/smo-object-model.md)  
  
  
