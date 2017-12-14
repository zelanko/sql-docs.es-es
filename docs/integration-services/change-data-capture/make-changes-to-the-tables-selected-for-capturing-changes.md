---
title: Realizar cambios en las tablas seleccionadas para capturar cambios | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: change-data-capture
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: makChanToTab
ms.assetid: a309f82a-c6ef-464d-a6ef-df555bfb609a
caps.latest.revision: "6"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4d6df6c0e20cb81a1525998da5934637d6ad6c29
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="make-changes-to-the-tables-selected-for-capturing-changes"></a>Realizar cambios en las tablas seleccionadas para capturar cambios
  En este cuadro de diálogo, puede seleccionar determinadas columnas de la tabla seleccionada desde las que se van a capturar datos. También puede editar la información de **Rol de seguridad** y de **Instancia de captura** .  
  
 Puede realizar los cambios siguientes en las tablas seleccionadas para capturar cambios en este cuadro de diálogo.  
  
 **Realizar cambios a las columnas incluidas en la instancia CDC:**  
  
 Realice una o ambas de las acciones siguientes:  
  
-   Active la casilla situada junto a cualquier columna adicional que desee incluir.  
  
-   Desactive la casilla situada junto a cualquier columna que ya no desee incluir.  
  
 **Cambiar el tipo de datos para una columna específica**:  
  
 Puede seleccionar un tipo de datos diferente para una columna determinada. Solo puede cambiar el tipo de datos a uno que sea compatible con el tipo de datos original.  
  
 Para cambiar el tipo de datos, haga clic en la columna **Tipo de datos** y seleccione un tipo de datos diferente. Solo están disponibles los tipos de datos compatibles con el tipo de datos original.  
  
> [!NOTE]  
>  Si no se puede seleccionar ningún tipo de datos adicional, la lista desplegable no estará disponible.  
  
 **Cambiar el rol de seguridad**  
  
 Escriba un nuevo nombre o edite el nombre del rol de acceso de seguridad en el campo **Rol de seguridad** .  
  
 **Cambiar o agregar una instancia de captura**  
  
 En el campo **Instancia de captura** , escriba un nombre para la instancia de captura.  
  
## <a name="see-also"></a>Vea también  
 [Cómo crear la instancia de base de datos de cambios de SQL Server](../../integration-services/change-data-capture/how-to-create-the-sql-server-change-database-instance.md)   
 [Seleccione las columnas y tablas de Oracle ](../../integration-services/change-data-capture/select-oracle-tables-and-columns.md)  
  
  
