---
title: Seleccionar tablas de Oracle para capturar cambios | Microsoft Docs
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
- selOraTabDia
ms.assetid: 2e295dc8-999d-4c4d-96cc-1519674b47a4
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: b0101c490f589e359b821edc2878a72969996d96
ms.sourcegitcommit: cc46afa12e890edbc1733febeec87438d6051bf9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/12/2018
ms.locfileid: "35409547"
---
# <a name="select-oracle-tables-for-capturing-changes"></a>Seleccionar tablas de Oracle para capturar cambios
  Use este cuadro de diálogo para seleccionar las tablas incluidas en la instancia CDC. Las tablas seleccionadas se agregarán a la lista de la página **Seleccionar tablas y columnas** del Asistente para nueva instancia. Puede hacer lo siguiente en este cuadro de diálogo.  
  
 De forma predeterminada, no se incluye ninguna tabla en la lista de tablas de este cuadro de diálogo. Puede activar la casilla situada en la parte superior de la columna de casilla para seleccionar todas las tablas o buscar determinadas tablas.  
  
 **Para buscar tablas específicas**  
 Escriba los criterios de búsqueda como se indica aquí y, después, haga clic en **Buscar**:  
  
-   **Esquema**: seleccione un esquema de base de datos de la lista. En la lista solo se incluirán las tablas que tengan dicho esquema.  
  
-   **Patrón de nombre de tabla**: escriba cualquier cadena de caracteres. Solo se mostrarán las tablas que incluyan la cadena de caracteres especificada.  
  
> [!NOTE]  
>  Puede especificar criterios en uno o ambos campos.  
  
-   **Mostrar las 1000 primeras tablas coincidentes**: de forma predeterminada, esta casilla está activada. Limita la presentación a las 1000 primeras tablas coincidentes. Si se desactiva la casilla, se mostrarán todas las tablas que cumplan los criterios. Si hay un gran número de tablas, se puede tardar mucho tiempo en mostrar la lista.  
  
 **Para seleccionar las tablas que se van a incluir en la instancia CDC**  
 Haga clic en la casilla situada junto a cualquiera de las tablas que quiera incluir y, después, haga clic en **Agregar**. Las tablas se agregarán a la lista de la página **Seleccionar tablas y columnas** del Asistente para nueva instancia.  
  
 Haga clic en **Cerrar** para cerrar el cuadro de diálogo sin agregar ninguna tabla adicional.  
  
> [!NOTE]  
>  Si selecciona una tabla que incluye un tipo de datos no admitido, verá un mensaje de error y la tabla no se incluirá.  
  
## <a name="see-also"></a>Ver también  
 [Cómo crear la instancia de base de datos de cambios de SQL Server](../../integration-services/change-data-capture/how-to-create-the-sql-server-change-database-instance.md)   
 [Seleccione las columnas y tablas de Oracle ](../../integration-services/change-data-capture/select-oracle-tables-and-columns.md)  
  
  
