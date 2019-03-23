---
title: Editar tablas | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- tabProps
ms.assetid: fed8fada-2abc-45e2-8228-0656f9c599cb
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 4c80f562b36e775ebcbbb3dd30a97fdb0bf61cb9
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/22/2019
ms.locfileid: "58385984"
---
# <a name="edit-tables"></a>Editar tablas
  Use la pestaña **Tablas** para realizar cambios en las tablas y columnas que seleccionó en la base de datos de origen de Oracle. Esta pestaña contiene los elementos siguientes:  
  
 **Lista de la tabla**  
 La lista de tablas tiene tres columnas:  
  
-   **Nombre de la tabla de Oracle**: El nombre de la tabla, incluido el esquema de tabla.  
  
-   **Instancia de captura**: El nombre de la instancia de captura que se usan como nombres de objetos de captura de datos modificados específicos de una instancia. La instancia de captura no puede ser NULL. Si no se especifica, el nombre deriva del nombre del esquema de origen más el nombre de la tabla de origen, con el formato `<schema-name>_<table-name>.` . El nombre de la instancia de captura no puede tener más de 100 caracteres y debe ser único dentro de la base de datos. Puede hacer clic en cualquier celda de esta columna para editar manualmente **capture_instance**.  
  
-   **Rol de seguridad**: El nombre del rol de base de datos utilizado para obtener acceso a datos modificados. Puede hacer clic en cualquier celda de esta columna para editar manualmente **security_role**.  
  
 **Agregar tablas**  
 Haga clic en **Agregar tablas** para abrir el cuadro de diálogo Selección de tabla, donde puede [Agregar tablas a una instancia CDC](add-tables-to-a-cdc-instance.md). La primera vez que tenga acceso a la base de datos de Oracle en esta sesión, debe [Connect to Oracle](connect-to-oracle.md).  
  
 **Editar**  
 Seleccione una tabla de la lista y haga clic en **Editar** para abrir el cuadro de diálogo **Propiedades** de la tabla, donde puede [Editar las propiedades de tabla](edit-the-table-properties.md).  
  
> [!NOTE]  
>  No puede editar la asignación de tipos para las tablas que ya tienen tablas reflejadas. Solo puede hacerlo para las tablas nuevas.  
  
 **Quitar**  
 Seleccione una tabla de la lista y haga clic en **Quitar** para quitar la tabla de la instancia CDC.  
  
## <a name="see-also"></a>Vea también  
 [Cómo editar las propiedades de la instancia CDC](how-to-edit-the-cdc-instance-properties.md)   
 [Seleccione las columnas y tablas de Oracle ](select-oracle-tables-and-columns.md)  
  
  
