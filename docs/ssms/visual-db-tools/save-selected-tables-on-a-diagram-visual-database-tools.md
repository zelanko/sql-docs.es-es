---
description: Guardar tablas seleccionadas en un diagrama (Visual Database Tools)
title: Guardar las tablas seleccionadas en un diagrama
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- saving tables
ms.assetid: 86943b49-48f3-432c-8021-928c13edfbcf
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.openlocfilehash: 9aea9e1ec6db770bc7c44f8b7a790c0564773beb
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88460029"
---
# <a name="save-selected-tables-on-a-diagram-visual-database-tools"></a>Guardar tablas seleccionadas en un diagrama (Visual Database Tools)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
Puede guardar una tabla específica o un conjunto de tablas si no desea guardar todos los cambios que haya realizado en un diagrama de base de datos.  
  
### <a name="to-save-selected-tables"></a>Para guardar tablas seleccionadas  
  
1.  En el diagrama de base de datos, seleccione las tablas que desea guardar.  
  
2.  En el menú **Archivo** , elija **Guardar selección**.  
  
3.  En el cuadro de diálogo **Guardar** , se muestra la lista de tablas que se actualizarán en la base de datos cuando guarde la selección.  
  
    Elija **Guardar archivo de texto** si desea guardar la lista de tablas en un archivo de texto del directorio del proyecto antes de continuar.  
  
4.  En el cuadro de diálogo **Guardar** , confirme la lista de tablas y elija **Sí** para guardar estas tablas.  
  
    > [!NOTE]  
    > La lista de tablas puede contener otras tablas además de las seleccionadas. Por ejemplo, si cambia el tipo de datos de una columna que participa en una relación con otra tabla, se incluirán las dos tablas en esta lista.  
  
## <a name="see-also"></a>Consulte también  
[Trabajar con diagramas de bases de datos](../../ssms/visual-db-tools/work-with-database-diagrams-visual-database-tools.md)  
  
