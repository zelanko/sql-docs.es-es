---
title: Ver el esquema del cubo | Documentos de Microsoft
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 51f22eecc2cc892d65691b13edb9382f3134ddac
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
ms.locfileid: "34022292"
---
# <a name="view-the-cube-schema"></a>Ver el esquema del cubo
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  El panel **Vista del origen de datos** de la pestaña **Estructura de cubo** del **Diseñador de cubos** muestra el esquema del cubo. El esquema es el conjunto de tablas de las que se derivan las medidas y las dimensiones de un cubo. Cada esquema de cubo se compone de una o varias tablas de hechos y una o varias tablas de dimensiones en las que se basan las medidas y las dimensiones del cubo.  
  
 El panel **Vista del origen de datos** de la pestaña **Estructura de cubo** muestra un diagrama de la vista del origen de datos en la que se basa el cubo. Este diagrama es un subconjunto del diagrama principal de la vista del origen de datos. Puede ocultar y mostrar tablas en el panel **Vista del origen de datos** y ver los diagramas existentes. Sin embargo, no puede realizar cambios (como agregar nuevas relaciones o consultas con nombre) al esquema subyacente. Para realizar cambios en el esquema, use el Diseñador de vistas del origen de datos.  
  
 Al crear un cubo, el diagrama que se muestra en el panel **Vista del origen de datos** de la pestaña **Estructura de cubo** es inicialmente el mismo que el diagrama **Mostrar todas las tablas** de la vista del origen de datos para el proyecto o la base de datos. Puede reemplazar este diagrama por cualquier diagrama existente en la vista del origen de datos y realizar ajustes en el panel **Vista del origen de datos** .  
  
 Cuando se trabaja con el diagrama en el **Diseñador de cubos**, los comandos que actúan sobre la pestaña o sobre cualquier objeto seleccionado en la pestaña están disponibles en el menú **Vista del origen de datos** . También puede hacer clic con el botón secundario en el fondo del diagrama o en cualquier objeto del diagrama para usar comandos que actúan sobre el diagrama o el objeto seleccionado. Puede hacer lo siguiente:  
  
-   Cambiar entre el formato de diagrama y el de árbol.  
  
-   Organizar, buscar, mostrar y ocultar tablas.  
  
-   Mostrar nombres descriptivos.  
  
-   Cambiar de diseño.  
  
-   Cambiar la ampliación (zoom).  
  
-   Ver las propiedades.  
  
 Además, puede realizar las acciones que se muestran en la tabla siguiente:  
  
|Para|Haga esto|  
|--------|-------------|  
|Usar un diagrama desde la vista del origen de datos del cubo|En el menú **Vista del origen de datos** , seleccione **Copiar diagrama desde**y, a continuación, haga clic en el diagrama de la vista del origen de datos que desea usar.<br /><br /> O bien<br /><br /> Haga clic con el botón derecho en el fondo del panel **Vista del origen de datos** , seleccione **Copiar diagrama desde**y, después, haga clic en el diagrama de la vista del origen de datos que prefiera. Este método crea una copia independiente del diagrama, de modo que los cambios que realice en la pestaña **Generador de cubos** no aparecen en el diagrama original.|  
|Mostrar solo las tablas usadas en el cubo|En el menú **Vista del origen de datos** , haga clic en **Mostrar solo tablas usadas**.<br /><br /> O bien<br /><br /> Haga clic con el botón derecho en el fondo del panel **Vista del origen de datos** y, después, haga clic en **Mostrar solo tablas usadas**.|  
|Editar el esquema de la vista del origen de datos|En el menú **Vista del origen de datos** , haga clic en **Editar vista del origen de datos**.<br /><br /> O bien<br /><br /> Haga clic con el botón derecho en el fondo del panel **Vista del origen de datos** y, después, haga clic en **Editar vista del origen de datos**.|  
  
  
