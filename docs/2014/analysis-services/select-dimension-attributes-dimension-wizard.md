---
title: Seleccionar atributos de dimensión (Asistente para dimensiones) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.dimensionwizard.dimensionattributes.f1
ms.assetid: f58a3e14-ab27-44d3-8c26-f5c9ee7583b0
author: minewiskan
ms.author: owend
ms.openlocfilehash: dcaf18ea2df3bbd3b227c8948d2fb15f54828853
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/09/2020
ms.locfileid: "84537927"
---
# <a name="select-dimension-attributes-dimension-wizard"></a>Seleccionar los atributos de la dimensión (Asistente para dimensiones)
  Utilice la página **Seleccionar los atributos de la dimensión** para seleccionar y modificar los atributos para la dimensión que debe crearse.  
  
> [!NOTE]  
>  Si no puede leer los valores de cualquier columna, maximice la ventana del asistente y cambie el ancho de cada encabezado de columna hasta que lea los valores.  
  
 **Para abrir el Asistente para dimensiones**  
  
-   En [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], en el **Explorador de soluciones**, haga clic con el botón derecho en la carpeta **Dimensiones** para un proyecto de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] y, luego, haga clic en **Nueva dimensión**.  
  
## <a name="options"></a>Opciones  
 (Columna con casillas)  
 Active las casillas para incluir atributos en la dimensión.  
  
 Para incluir un atributo específico, active la casilla de dicho atributo.  
  
 Para incluir todos los atributos, active la casilla del encabezado de la columna.  
  
> [!NOTE]  
>  No se puede desactivar la casilla para el atributo clave.  
  
 **Nombre del atributo**  
 Enumera los atributos disponibles.  
  
 Para cambiar el nombre de un atributo, haga clic en el nombre del atributo y escriba otro nombre.  
  
 **Habilitar exploración**  
 Seleccione esta opción para que el atributo esté disponible para que el usuario final pueda examinar y filtrar. La opción**Habilitar exploración** debe estar seleccionada para el atributo clave. Para los atributos no clave, el valor predeterminado es no tener la opción **Habilitar exploración** seleccionada, lo que hace que se muestren los atributos no clave solo como propiedades de miembro.  
  
 En la mayoría de los casos, el atributo se convierte en disponible o no disponible para examinar estableciendo la propiedad `AttributeHierarchyEnabled` en `True` o `False`, respectivamente. Sin embargo, en los tres casos siguientes, el asistente usa valores diferentes.  
  
|Caso|Configuración|  
|----------|--------------|  
|Una dimensión contiene una jerarquía de elementos primarios y secundarios, y la opción **Habilitar exploración** no está seleccionada|El asistente deja la propiedad `AttributeHierarchyEnabled` establecida en `True`y establece el atributo `AttributeHierarchyVisible` en `False` para el atributo clave.|  
|Una tabla de una dimensión contiene una clave externa a una tabla que no se encuentra en la dimensión.|El asistente selecciona la clave externa como un atributo que se va a incluir pero no seleccionará **Habilitar exploración**. Si mantiene esta configuración, la propiedad `AttributeHiearchyEnabled` del atributo se establecerá en `True`y la propiedad `AttributeHierarchyVisible` se establecerá en `False`.|  
|Una dimensión contiene tablas de copo de nieve a las que se tiene acceso a través de columnas de clave externa que admiten valores NULL<br /><br /> \- y -<br /><br /> la opción Habilitar exploración para el atributo que está basado en la clave de la tabla de copo de nieve no está seleccionada.|El asistente creará el nuevo atributo que tiene la propiedad `AttributeHiearchyEnabled` establecida en `True`y la propiedad `AttributeHierarchyVisible` establecida en `False`.|  
  
 **Tipo de atributo**  
 (Opcional) Establezca el tipo para el atributo. El valor predeterminado es **Regular**. El tipo de atributo proporciona orientación a las aplicaciones cliente sobre qué información podría contener el atributo.  
  
## <a name="see-also"></a>Consulte también  
 [Asistente para dimensiones (ayuda F1)](dimension-wizard-f1-help.md)   
 [Dimensiones &#40;Analysis Services de datos multidimensionales&#41;](multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data.md)   
 [Dimensiones en modelos multidimensionales](multidimensional-models/dimensions-in-multidimensional-models.md)  
  
  
