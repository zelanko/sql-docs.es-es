---
description: Realizar cambios en las tablas seleccionadas para capturar cambios
title: Realizar cambios en las tablas seleccionadas para capturar cambios | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- makChanToTab
ms.assetid: a309f82a-c6ef-464d-a6ef-df555bfb609a
author: chugugrace
ms.author: chugu
ms.openlocfilehash: b6caa3f5d6d1abe5a8d4a197391da18a74942f00
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88394491"
---
# <a name="make-changes-to-the-tables-selected-for-capturing-changes"></a>Realizar cambios en las tablas seleccionadas para capturar cambios

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


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
  
## <a name="see-also"></a>Consulte también  
 [Cómo crear la instancia de base de datos de cambios de SQL Server](../../integration-services/change-data-capture/how-to-create-the-sql-server-change-database-instance.md)   
 [Seleccionar tablas y columnas de Oracle](../../integration-services/change-data-capture/select-oracle-tables-and-columns.md)  
  
  
