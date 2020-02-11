---
title: Crear conjuntos con nombre | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- calculations [Analysis Services], named sets
- named sets [Analysis Services]
- members [Analysis Services], named sets
ms.assetid: 03cf97a4-1a18-45f3-acb0-35123bd619be
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c1fc4ab5d778535fdc4e2186c5bc88741b4367f5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66076142"
---
# <a name="create-named-sets"></a>Crear conjuntos con nombre
  Un conjunto con nombre es un conjunto de miembros de dimensión o una expresión de conjunto que se crea para volver a usarse en, por ejemplo, consultas de expresiones multidimensionales (MDX). Puede crear conjuntos con nombre combinando datos del cubo, operadores aritméticos, números y funciones. Por ejemplo, puede crear un conjunto con nombre llamado Top Ten Factories, que contenga los diez miembros de la dimensión Factories con los valores superiores de la medida Production. Acto seguido, puede utilizar Top Ten Factories en las consultas de los usuarios finales. Por ejemplo, un usuario final puede colocar Top Ten Factories en un eje y la dimensión Measures, incluyendo a Production, en otro. Para más información, vea [Cálculos en modelos multidimensionales](calculations-in-multidimensional-models.md) y [Crear conjuntos con nombre en MDX &#40;MDX&#41;](mdx/mdx-named-sets-building-named-sets.md).  
  
 Para crear un conjunto con nombre, utilice el comando **Nuevo conjunto con nombre** en la pestaña **Cálculos** del Diseñador de cubos. Este comando se puede invocar en el menú **Cubo** de la barra de herramientas de la pestaña **Cálculos** . Este comando muestra un formulario para especificar las siguientes opciones para el conjunto con nombre:  
  
 **Nombre**  
 Seleccione el nombre del conjunto con nombre. Éste es el nombre que ven los usuarios finales cuando examinan el cubo.  
  
 **Expression**  
 Especifique la expresión que crea el conjunto con nombre. Esta expresión puede escribirse en MDX. La expresión puede contener cualquiera de los elementos siguientes:  
  
-   Expresiones de datos que representan los componentes del cubo como dimensiones, niveles, medidas, etc.  
  
-   Operadores aritméticos.  
  
-   Números.  
  
-   Funciones.  
  
 Puede copiar o arrastrar los componentes del cubo desde la pestaña **Metadatos** del panel **Herramientas de cálculo** hasta el cuadro **Expresión** del panel **Editor de Formulario de conjuntos con nombres** . Puede copiar o arrastrar funciones desde la pestaña **Funciones** del panel **Herramientas de cálculo** al cuadro **Expresión** del panel **Editor de Formulario de conjuntos con nombres** .  
  
> [!IMPORTANT]  
>  Si crea la expresión de conjunto mediante el nombre explícito de los miembros del conjunto, incluya la lista de miembros en un par de llaves ({}).  
  
## <a name="see-also"></a>Consulte también  
 [Cálculos en modelos multidimensionales](calculations-in-multidimensional-models.md)  
  
  
