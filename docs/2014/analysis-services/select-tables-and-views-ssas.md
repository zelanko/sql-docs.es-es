---
title: Seleccionar tablas y vistas (SSAS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.seltablesviews.f1
ms.assetid: 5e8121cc-03f0-4168-98cf-63c5c032bb0b
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8ff8ada00af8b70659a19f863a52a5f1005e20b4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66069237"
---
# <a name="select-tables-and-views-ssas"></a>Seleccionar tablas y vistas (SSAS)
  Esta página del **Asistente para la importación de tablas** le permite seleccionar las tablas y vistas de las que desea importar los datos. Para tener acceso al asistente desde [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], en el menú **Modelo** , haga clic en **Importar desde el origen de datos**.  
  
 El hecho de que aparezcan tablas y vistas en esta página no garantiza que la importación se realizará correctamente. Si el usuario especificado en la página Información de suplantación no tiene privilegios suficientes para leer la base de datos seleccionada, la importación no se realizará correctamente.  
  
 Para los orígenes de datos que usan la autenticación de Windows, se utilizan las credenciales del usuario actual para capturar las tablas y vistas del cuadro de diálogo en Seleccionar tablas y vistas. Para capturar los datos de los demás orígenes de datos se usan las credenciales proporcionadas en la cadena de conexión.  
  
## <a name="uielement-list"></a>Lista de UIElement  
 **Server**  
 Muestra el servidor con que está conectado.  
  
 **Base de datos**  
 Muestra la base de datos que seleccionó.  
  
 **Tablas y vistas**  
 Enumera las tablas y vistas de la base de datos. Active la casilla situada al lado de cada tabla y vista que desee importar.  
  
 **Tabla de origen**  
 Especifica el nombre de la tabla de origen basado en el tipo de origen de datos.  
  
 **Esquema**  
 Especifica el esquema en el que está la tabla de origen. En función del tipo de base de datos, un esquema funciona como un contenedor para otros objetos, como tablas, y también puede indicar la propiedad de esos objetos.  
  
 **Nombre descriptivo**  
 Especifica el nombre descriptivo de la tabla de origen. De forma predeterminada, la columna muestra el nombre de la tabla de origen que aparece en la columna **Tabla de origen** . Cambie el nombre si desea utilizar un nombre distinto del que se usa en la base de datos de origen.  
  
 **Detalles del filtro**  
 Cuando se ha aplicado un filtro a los datos que se están importando, muestra el filtro de importación de datos en el cuadro de diálogo **Detalles del filtro**. Para obtener más información, vea [Detalles del filtro &#40;SSAS&#41;](filter-details-ssas.md).  
  
 **Vista previa y filtrar**  
 Muestra el cuadro de diálogo **Vista previa de la tabla seleccionada** que se usa para aplicar un filtro a los datos que se están importando. Para obtener más información, consulte [Vista previa de la tabla seleccionada &#40;SSAS&#41;](preview-selected-table-ssas.md).  
  
 **Seleccionar tablas relacionadas**  
 Se importan las tablas y vistas que se relacionan con las tablas y vistas que ha seleccionado.  
  
  
