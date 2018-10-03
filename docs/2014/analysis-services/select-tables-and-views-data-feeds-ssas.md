---
title: Seleccionar tablas y vistas (fuentes de datos) (SSAS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.seltablesviewsdf.f1
ms.assetid: 6c4fafe0-e02e-47d1-b8bc-e70e872690af
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7e7d17866842671cebf87ee8f1e44803fe1bb463
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48224913"
---
# <a name="select-tables-and-views-data-feeds-ssas"></a>Seleccionar tablas y vistas (fuentes de distribución de datos) (SSAS)
  Esta página del **Asistente para la importación de tablas** le permite seleccionar las tablas y vistas de las que desea importar los datos. Para tener acceso al asistente desde [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], en el menú **Modelo** , haga clic en **Importar desde el origen de datos**.  
  
 El hecho de que aparezcan tablas y vistas en esta página no garantiza que la importación se realizará correctamente. Si el usuario especificado en la página Información de suplantación no tiene privilegios suficientes para leer la base de datos seleccionada, la importación no se realizará correctamente.  
  
 Para los orígenes de datos que usan la autenticación de Windows, se utilizan las credenciales del usuario actual para capturar las tablas y vistas del cuadro de diálogo en Seleccionar tablas y vistas. Para capturar los datos de los demás orígenes de datos se usan las credenciales proporcionadas en la cadena de conexión.  
  
## <a name="uielement-list"></a>Lista de UIElement  
 **Dirección URL de fuente de datos**  
 Muestra la dirección URL para la fuente de distribución de datos que seleccionó.  
  
 **Las tablas y vistas**  
 Enumera las tablas y vistas de la fuente de datos. Active la casilla situada al lado de cada tabla y vista que desee importar.  
  
 **Tabla de origen**  
 Especifica el nombre de la tabla de origen basado en el tipo de origen de datos.  
  
 **Nombre descriptivo**  
 Especifica el nombre descriptivo de la tabla de origen. De forma predeterminada, la columna muestra el nombre de la tabla de origen que aparece en la columna **Tabla de origen** .  
  
 **Detalles del filtro**  
 Muestra el filtro de importación de datos en el cuadro de diálogo **Detalles del filtro**, cuando se ha aplicado un filtro a los datos que se están importando. Para obtener más información, vea [Detalles del filtro &#40;SSAS&#41;](filter-details-ssas.md).  
  
 **Vista previa y filtrar**  
 Muestra el cuadro de diálogo **Vista previa de la tabla seleccionada** que se usa para aplicar un filtro a los datos que se están importando. Para obtener más información, consulte [Vista previa de la tabla seleccionada &#40;SSAS&#41;](preview-selected-table-ssas.md).  
  
 **Seleccionar tablas relacionadas**  
 Seleccionar las tablas que se relacionan con las tablas y vistas que ha seleccionado.  
  
  
