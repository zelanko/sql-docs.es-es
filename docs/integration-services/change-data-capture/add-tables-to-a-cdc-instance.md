---
title: Agregar tablas a una instancia CDC | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- addTabs
ms.assetid: ad260e19-c021-4035-9311-c02fc96ceaea
caps.latest.revision: 9
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 1e4cf4488c795dd2cf3a4ffaade2fb5579424eeb
ms.sourcegitcommit: de5e726db2f287bb32b7910831a0c4649ccf3c4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/12/2018
ms.locfileid: "35328179"
---
# <a name="add-tables-to-a-cdc-instance"></a>Agregar tablas a una instancia CDC
  Use el cuadro de diálogo Selección de tablas para agregar tablas adicionales del origen de Oracle a la instancia CDC. Las tablas seleccionadas se agregarán a la lista de la pestaña **Tablas** del editor de propiedades.  
  
 De forma predeterminada, no se incluye ninguna tabla en la lista de tablas de este cuadro de diálogo. Puede activar la casilla **(Seleccionar todo)** o buscar tablas específicas.  
  
 **Para buscar tablas específicas**  
 Escriba los criterios de búsqueda como se indica aquí y, después, haga clic en **Buscar**:  
  
-   **Esquema**: seleccione un esquema de base de datos de la lista. En la lista solo se incluirán las tablas que tengan dicho esquema.  
  
-   **Patrón de nombre de tabla**: escriba cualquier cadena de caracteres. Solo se mostrarán las tablas que incluyan la cadena de caracteres especificada.  
  
> [!NOTE]  
>  Puede especificar criterios en uno o ambos campos.  
  
-   **Mostrar las 1000 primeras tablas coincidentes**: de forma predeterminada, esta casilla está activada. Limita la presentación a las 1000 primeras tablas coincidentes. Si se desactiva la casilla, se mostrarán todas las tablas que cumplan los criterios. Si hay un gran número de tablas, se puede tardar mucho tiempo en mostrar la lista.  
  
 **Para seleccionar las tablas que se van a incluir en la instancia CDC**  
 Haga clic en la casilla situada junto a cualquiera de las tablas que quiera incluir y, después, haga clic en **Agregar**. Las tablas se agregarán a la lista de la página **Seleccionar tablas y columnas** del Asistente para nueva instancia.  
  
 Haga clic en **Cerrar** para cerrar el cuadro de diálogo sin agregar ninguna tabla.  
  
> [!NOTE]  
>  Si selecciona una tabla que incluye un tipo de datos no admitido, verá un mensaje de error y la tabla no se incluirá.  
  
> [!NOTE]  
>  Puede ver la lista de tablas en el visor. Cuando se usa el visor, la información es de solo lectura. El visor también incluye una lista de las columnas capturadas de la tabla. Para obtener información acerca de cómo obtener acceso al visor, vea [How to Manage a CDC Instance](../../integration-services/change-data-capture/how-to-manage-a-cdc-instance.md).  
  
## <a name="see-also"></a>Ver también  
 [Cómo editar las propiedades de la instancia CDC](../../integration-services/change-data-capture/how-to-edit-the-cdc-instance-properties.md)   
 [Cómo administrar una instancia CDC](../../integration-services/change-data-capture/how-to-manage-a-cdc-instance.md)   
 [Seleccionar tablas de Oracle para capturar cambios ](../../integration-services/change-data-capture/select-oracle-tables-for-capturing-changes.md)  
  
  
