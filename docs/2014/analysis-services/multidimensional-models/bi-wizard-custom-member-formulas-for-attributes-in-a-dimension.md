---
title: Establecer fórmulas de miembro personalizado para los atributos de una dimensión | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Business Intelligence enhancements [Analysis Services], custom member formulas
- member formulas [Analysis Services]
- dimensions [Analysis Services], Business Intelligence enhancements
- custom member formulas [Analysis Services]
- CustomRollupColumn property
ms.assetid: c4467b08-ce59-4de7-a2d9-c22e246bdd52
author: minewiskan
ms.author: owend
ms.openlocfilehash: 112f8944bd20b2b6a464b0d84fb8ac1a0e89d976
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/09/2020
ms.locfileid: "84544577"
---
# <a name="set-custom-member-formulas-for-attributes-in-a-dimension"></a>Configurar fórmulas de miembro personalizado para los atributos de una dimensión
  Agregar una fórmula de miembro personalizado a un cubo o dimensión para reemplazar la agregación predeterminada asociada a un miembro de dimensión con los resultados de una expresión de Expresiones multidimensionales (MDX). (Esta mejora establece la propiedad `CustomRollupColumn` en un atributo especificado en una dimensión).  
  
> [!NOTE]  
>  Hay una fórmula de miembro personalizado disponible solamente para dimensiones que se basan en orígenes de datos existentes. Para las dimensiones creadas sin usar un origen de datos, debe ejecutar el Asistente para generar esquemas para crear una vista del origen de datos antes de agregar una fórmula de miembro personalizado.  
  
 Para agregar una fórmula de miembro personalizado, se usa el Asistente de Business Intelligence y se selecciona la opción **Crear una fórmula de miembro personalizado** en la página **Elegir mejora** . A continuación, este asistente le guía por los pasos para seleccionar una dimensión a la que desee aplicar una fórmula de miembro personalizado y habilitar dicha fórmula.  
  
## <a name="selecting-a-dimension"></a>Seleccionar una dimensión  
 En la primera página del asistente **Crear una fórmula de miembro personalizado** se especifica la dimensión a la que se desea aplicar una fórmula de miembro personalizado. La mejora de fórmula de miembro personalizado agregada a esta dimensión seleccionada produce cambios en la dimensión. Estos cambios son heredados por todos los cubos que incluyan la dimensión seleccionada.  
  
## <a name="enabling-a-custom-member-formula"></a>Habilitar una fórmula de miembro personalizado  
 En la segunda página de **Crear una fórmula de miembro personalizado** , se asocia la columna de origen que contiene la fórmula de miembro personalizado a uno o más atributos de la dimensión. En la columna **Atributo** , se activa la casilla situada junto al atributo que se desea asociar a la columna de fórmula de miembro personalizado. Después de seleccionar cada atributo, el asistente muestra un cuadro de diálogo **Seleccionar una columna** . En este cuadro de diálogo, haga clic en la columna de la tabla de dimensiones que contiene la fórmula. Si quiere cambiar la selección después de cerrar el cuadro de diálogo **Seleccionar una columna** , haga clic en la celda **Columna de origen** que quiera cambiar y haga clic en el botón de puntos suspensivos (**…**) para volver a abrir el cuadro de diálogo **Seleccionar una columna** .  
  
## <a name="see-also"></a>Consulte también  
 [Usar el Asistente de Business Intelligence para mejorar dimensiones](../use-the-business-intelligence-wizard-to-enhance-dimensions.md)  
  
  
