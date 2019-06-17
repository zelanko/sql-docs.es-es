---
title: Seleccionar tablas y columnas de Oracle | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- selTabCol
ms.assetid: bf73f80e-a954-4c5f-874e-17fdd4082715
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: fe951cb7811bb8cc92414564fda466657d2fae8c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62771061"
---
# <a name="select-oracle-tables-and-columns"></a>Seleccionar tablas y columnas de Oracle
  Use la página Seleccionar tablas y columnas de Oracle para seleccionar las tablas de la base de datos de origen de Oracle donde se capturan cambios. Esta página contiene los elementos siguientes:  
  
## <a name="options"></a>Opciones  
 **Lista de tablas**  
 La lista de tablas tiene tres columnas:  
  
-   **Nombre de la tabla de Oracle**: nombre de la tabla, incluido el esquema de tabla.  
  
-   **Instancia de captura**: el nombre de la instancia de captura que se usa para denominar los objetos de captura de datos modificados específicos de una instancia. La instancia de captura no puede ser NULL.  
  
     Si no se especifica, el nombre se obtiene del nombre del esquema de origen al que se agrega el nombre de la tabla de origen en el formato `<schema-name>_<table-name>`. El nombre de la instancia de captura no puede tener más de 100 caracteres y debe ser único dentro de la base de datos.  
  
     Puede hacer clic en cualquier celda de esta columna para editar manualmente **capture_instance**.  
  
-   **Rol de seguridad**: nombre del rol de acceso de base de datos usado para controlar el acceso a los datos modificados.  
  
     Puede hacer clic en cualquier celda de esta columna para editar manualmente **security_role**.  
  
 **Agregar tablas**  
 Haga clic en **Agregar tablas** para abrir el cuadro de diálogo Selección de tabla, donde puede [Seleccionar tablas de Oracle para capturar cambios](select-oracle-tables-for-capturing-changes.md).  
  
 **Editar**  
 Seleccione una tabla de la lista y seleccione **Editar** para abrir el cuadro de diálogo **Propiedades** de la tabla, donde puede [Realizar cambios en las tablas seleccionadas para capturar cambios](make-changes-to-the-tables-selected-for-capturing-changes.md).  
  
 **Quitar**  
 Seleccione una tabla de la lista y haga clic en **Quitar** para quitar la tabla de la instancia CDC.  
  
 Después de [Seleccionar tablas de Oracle para capturar cambios](select-oracle-tables-for-capturing-changes.md) o [Realizar cambios en las tablas seleccionadas para capturar cambios](make-changes-to-the-tables-selected-for-capturing-changes.md) con los cuadros de diálogo correspondientes, haga clic en **Siguiente** para [Generar y ejecutar el script de registro complementario](generate-and-run-the-supplemental-logging-script.md).  
  
## <a name="see-also"></a>Vea también  
 [Cómo crear la instancia de base de datos de cambios de SQL Server](how-to-create-the-sql-server-change-database-instance.md)   
 [Editar tablas](edit-tables.md)   
 [Agregar tablas a una instancia CDC](add-tables-to-a-cdc-instance.md)   
 [Editar las propiedades de tabla](edit-the-table-properties.md)  
  
  
