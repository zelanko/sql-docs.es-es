---
title: El nombre coincidente (Data Source View Wizard) (Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.datasourceviewwizard.namematchingcriteria.f1
ms.assetid: 7f811e02-0fe6-45c9-a7b7-29c61032d96b
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4b3d122ba2c23202e44db7b0677062135ab7ba5e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62743650"
---
# <a name="name-matching-data-source-view-wizard-analysis-services"></a>Coincidencia de nombres (Asistente para vistas del origen de datos) (Analysis Services)
  Use la página **Coincidencia de nombres** para seleccionar el criterio que desea utilizar para detectar las posibles relaciones entre las tablas seleccionadas para la vista del origen de datos y las demás tablas del esquema. Si no existen relaciones de claves externas físicas entre las tablas, este criterio le permitirá identificar y agregar las tablas relacionadas a la vista del origen de datos. Las relaciones lógicas identificadas por la coincidencia de nombres también se agregan a la vista del origen de datos.  
  
> [!NOTE]  
>  Solo se mostrará esta página si selecciona un origen de datos con varias tablas que no presente relaciones de clave externa con las demás tablas.  
  
## <a name="options"></a>Opciones  
 **Crear relaciones lógicas por columnas coincidentes**  
 Seleccione esta opción para usar un criterio de coincidencia de nombres para detectar posibles dependencias y relaciones lógicas entre las tablas seleccionadas que desea incluir en la vista del origen de datos y las demás tablas del esquema. Si desactiva esta casilla, no se utilizará el criterio de coincidencia de nombres para identificar las relaciones lógicas entre las tablas del origen de datos.  
  
 **Coincidencias de claves externas**  
 Seleccione el criterio que desea utilizar para crear relaciones lógicas entre tablas y vistas en el origen de datos. Se ignorarán los caracteres que no sean alfanuméricos en las cadenas que desea hacer coincidir. Por ejemplo, se harán coincidir "Customer ID", "Customer_ID" y "CustomerID". Seleccione una de las opciones de la siguiente tabla para crear relaciones conforme a las condiciones especificadas.  
  
|Select|Para crear|  
|------------|---------------|  
|**Mismo nombre que el de la clave principal**|Una relación lógica con todas las tablas con un nombre de columna que coincida con el nombre de la columna de clave principal de la tabla seleccionada.|  
|**Mismo nombre que el nombre de tabla de destino**|Una relación lógica con todas las tablas con un nombre de columna que coincida con el nombre de la tabla seleccionada.|  
|**Nombre de la tabla de destino + nombre de la clave principal**|Una relación lógica con todas las tablas en las que el nombre de columna coincide con el nombre de la tabla seleccionada concatenada con el nombre de la columna de clave principal para la tabla seleccionada, por ese orden. Se ignorarán los caracteres que no sean alfanuméricos en la concatenación (por ejemplo, se harán coincidir "Product ID", "Product_ID" y "ProductID").|  
  
 **Descripción y muestra**  
 Vea una descripción y una muestra del criterio seleccionado.  
  
  
