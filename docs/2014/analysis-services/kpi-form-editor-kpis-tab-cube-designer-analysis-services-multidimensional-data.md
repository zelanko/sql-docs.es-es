---
title: Editor de formulario de KPI (pestaña KPI, Diseñador de cubos) (Analysis Services - datos multidimensionales) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubeeditor.kpidefinitionpane.f1
ms.assetid: 45c6453a-bbe2-4ca5-836e-c7ef11cfcb65
caps.latest.revision: 23
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 284ccc63f98624e1a64b114d31b69215d8e6b1be
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37224845"
---
# <a name="kpi-form-editor-kpis-tab-cube-designer-analysis-services---multidimensional-data"></a>Editor de Formulario de KPI (pestaña KPI, Diseñador de cubos) (Analysis Services - Datos multidimensionales)
  Use el panel **Editor de Formulario de KPI** de la pestaña **KPI** del Diseñador de cubos para crear o modificar el indicador clave de rendimiento (KPI) seleccionado.  
  
> [!NOTE]  
>  Este panel solo se muestra en la vista de formulario.  
  
## <a name="options"></a>Opciones  
 **Nombre**  
 Escriba el nombre del KPI.  
  
 **Grupo de medida asociado**  
 Seleccione el grupo de medida asociado con el KPI. La aplicación cliente puede utilizar esta información para determinar qué dimensiones están disponibles cuando el usuario examina este KPI.  
  
 **Expresión de valor**  
 Expanda para ver o editar la expresión MDX (Expresiones multidimensionales) para el valor del KPI.  
  
 Escriba la expresión MDX que devuelve el valor del KPI.  
  
 Arrastre los elementos seleccionados del panel **Herramientas de cálculo** hasta esta opción para incluir la sintaxis MDX para el elemento seleccionado.  
  
 **Expresión objetivo**  
 Expanda para ver o editar la expresión MDX para el valor objetivo del KPI.  
  
 Escriba la expresión MDX que devuelve el valor objetivo del KPI cuando éste se ejecuta.  
  
 Arrastre los elementos seleccionados del panel **Herramientas de cálculo** hasta esta opción para incluir la sintaxis MDX para el elemento seleccionado.  
  
 **Estado**  
 Expanda para ver las opciones **Gráfico de estado** y **Expresión de estado** .  
  
 **Gráfico de estado**  
 Seleccione el gráfico que utilizará la aplicación cliente para representar el valor de estado en forma gráfica.  
  
> [!NOTE]  
>  La aplicación cliente puede admitir el gráfico seleccionado o reemplazarlo con una alternativa adecuada.  
  
 **Expresión de estado**  
 Escriba la expresión MDX que devuelve el valor de estado del KPI cuando éste se ejecuta.  
  
 Arrastre los elementos seleccionados del panel **Herramientas de cálculo** hasta esta opción para incluir la sintaxis MDX para el elemento seleccionado.  
  
 Se recomienda que esta expresión devuelva un número decimal entre -1 y 1. Un número menor representa una situación negativa, mientras que un número mayor representa una situación positiva.  
  
> [!NOTE]  
>  Los valores inferiores a –1 y superiores a 1 son posibles, pero es posible que las aplicaciones cliente de terceros no los interpreten correctamente.  
  
 **Tendencia**  
 Expanda para ver las opciones **Gráfico de tendencia** y **Expresión de tendencia** .  
  
 **Gráfico de tendencia**  
 Seleccione el gráfico que utilizará la aplicación cliente para representar el valor de tendencia en forma gráfica.  
  
> [!NOTE]  
>  La aplicación cliente puede admitir el gráfico seleccionado o reemplazarlo con una alternativa adecuada.  
  
 **Expresión de tendencia**  
 Escriba la expresión MDX que devuelve el valor de tendencia del KPI.  
  
 Arrastre los elementos seleccionados del panel **Herramientas de cálculo** hasta esta opción para incluir la sintaxis MDX para el elemento seleccionado.  
  
 La expresión de tendencia puede basarse en cualquier criterio basado en el tiempo que tenga sentido en un contexto empresarial determinado. Se recomienda que esta expresión devuelva un número decimal entre -1 y 1. Un número menor representa una tendencia negativa a lo largo del tiempo; un número mayor representa una tendencia positiva a lo largo del tiempo.  
  
> [!NOTE]  
>  Los valores inferiores a –1 y superiores a 1 son posibles, pero es posible que las aplicaciones cliente de terceros no los interpreten correctamente.  
  
 **Propiedades adicionales**  
 Expanda para ver las opciones **Carpeta para mostrar**, **KPI primario**, **Miembro de hora actual**, **Peso**y **Descripción** .  
  
 **Carpeta para mostrar**  
 Escriba la categorización del KPI que se utilizará en la aplicación cliente para mostrarlo.  
  
 Use una barra inversa (\\) para separar nombres de carpetas en una carpeta para mostrar y un punto y coma (;) para separar varias carpetas para mostrar. Por ejemplo, escriba `Category\Goal\Scientific;Category\Goal\Metric`.  
  
 **KPI primario**  
 Seleccione un KPI existente en el que categorizar el KPI que se utilizará en la aplicación cliente.  
  
> [!NOTE]  
>  Si esta opción está establecida en un KPI existente, se omite **Carpeta para mostrar** .  
  
 **Miembro de hora actual**  
 Escriba la expresión MDX que devuelve el miembro que identifica el contexto temporal del KPI.  
  
 Arrastre los elementos seleccionados del panel **Herramientas de cálculo** hasta esta opción para incluir la sintaxis MDX para el elemento seleccionado.  
  
> [!IMPORTANT]  
>  La expresión MDX debe devolver el nombre único de un miembro en una dimensión de tiempo asociada con el grupo de medida especificado en **Grupo de medida asociado**.  
  
 **Weight**  
 Expanda para ver o editar la expresión MDX para el factor de peso del KPI.  
  
 Arrastre los elementos seleccionados del panel **Herramientas de cálculo** hasta esta opción para incluir la sintaxis MDX para el elemento seleccionado.  
  
 **Descripción**  
 Escriba la descripción opcional del KPI.  
  
## <a name="see-also"></a>Vea también  
 [KPI &#40;Diseñador de cubos&#41; &#40;Analysis Services - datos multidimensionales&#41;](kpis-cube-designer-analysis-services-multidimensional-data.md)  
  
  
