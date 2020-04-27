---
title: Vista previa de la tabla seleccionada (SSAS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.previewselecttable.f1
ms.assetid: b6b34b5a-43b3-4a75-9f3b-b2ad1084b1b6
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0a0f168dabd237fe685eb90d2caeeba0db4eed97
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "66070719"
---
# <a name="preview-selected-table-ssas"></a>Vista previa de la tabla seleccionada (SSAS)
  Esta página del **Asistente para la importación de tablas** le permite obtener una vista previa de los datos de la tabla seleccionada, seleccionar las columnas que se van a incluir en la importación de datos y filtrar los datos de las columnas seleccionadas. Para tener acceso al asistente desde [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], en el menú **Modelo** , haga clic en **Importar desde el origen de datos**.  
  
 No se muestran todas las filas de la tabla. Sin embargo, los filtros que establezca se aplicarán a todos los datos de la tabla durante la importación.  
  
 Para los orígenes de datos que usan la autenticación de Windows, se utilizan las credenciales del usuario actual para capturar los datos mostrados en el cuadro de diálogo Vista previa y aplicar filtro. Para capturar los datos de los demás orígenes de datos se usan las credenciales proporcionadas en la cadena de conexión.  
  
 El hecho de que aparezcan datos en esta página no garantiza que la importación se realizará correctamente. Si el nombre de usuario especificado en la página Información de suplantación no tiene privilegios suficientes para leer la base de datos seleccionada, la importación no se realizará correctamente.  
  
## <a name="uielement-list"></a>Lista de UIElement  
 **Casilla en el encabezado de columna**  
 Active la casilla para incluir la columna en la importación de datos. Desactive la casilla para quitar la columna de la importación de datos.  
  
 **Botón de flecha abajo en el encabezado de columna**  
 Filtre los datos de la columna.  
  
 **Borrar filtros de fila**  
 Quite todos los filtros que se aplicaron a los datos en las columnas.  
  
  
