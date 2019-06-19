---
title: Crear un cubo con el Asistente para cubos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- cubes [Analysis Services], creating
ms.assetid: d46d659c-3a4e-4364-94ac-f5eb6ba0ec25
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7ffd5880120184249d89c4d702b30c8d6e01e1f6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66076501"
---
# <a name="create-a-cube-using-the-cube-wizard"></a>Crear un cubo con el Asistente para cubos
  Puede crear un nuevo cubo usando el Asistente para cubos de [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
### <a name="to-create-a-new-cube"></a>Para crear un nuevo cubo  
  
1.  En el **Explorador de soluciones**, haga clic con el botón derecho en **Cubos**y, después, haga clic en **Nuevo cubo**.  
  
2.  En la página **Seleccionar método de creación** del Asistente para cubos, active la opción **Usar tablas existentes**y, a continuación, haga clic en **Siguiente**.  
  
    > [!NOTE]  
    >  Es posible que tenga que crear un cubo sin que sea necesario usar tablas existentes. Para crear un cubo vacío, seleccione **Crear un cubo vacío**. Para generar tablas, seleccione **Generar tablas en el origen de datos**.  
  
3.  En la página **Seleccionar tablas de grupos de medida** , realice los procedimientos siguientes:  
  
    1.  En la lista **Vista del origen de datos** , seleccione una vista del origen de datos.  
  
    2.  En la lista **Tablas de grupos de medida** , seleccione las tablas que se van a usar para crear grupos de medida.  
  
    3.  Haga clic en **Siguiente**.  
  
4.  En la página **Seleccionar medidas** , seleccione las medidas que desee incluir en el cubo y, a continuación, haga clic en **Siguiente**.  
  
     Si lo desea, puede cambiar los nombres de las medidas y de los grupos de medida.  
  
5.  En la página **Seleccionar dimensiones existentes** , seleccione las dimensiones existentes que se incluirán en el cubo y haga clic en **Siguiente**.  
  
    > [!NOTE]  
    >  La página **Seleccionar dimensiones existentes** aparece cuando ya existen dimensiones en la base de datos de cualquiera de los grupos de medida seleccionados.  
  
6.  En la página **Seleccionar nuevas dimensiones** , seleccione las nuevas dimensiones que se van a crear y, a continuación, haga clic en **Siguiente**.  
  
    > [!NOTE]  
    >  La página **Seleccionar nuevas dimensiones** se muestra cuando cualquier tabla es un buen candidato para las tablas de dimensiones y las dimensiones existentes aún no usan las tablas.  
  
7.  En la página **Seleccionar claves de dimensiones ausentes** , seleccione una clave para la dimensión y, a continuación, haga clic en **Siguiente**.  
  
    > [!NOTE]  
    >  La página **Seleccionar las claves de dimensión que faltan** se muestra cuando no se ha definido una clave para alguna de las tablas de dimensiones especificadas.  
  
8.  En la página **Finalización del asistente** , escriba un nombre para el nuevo cubo y revise la estructura del cubo. Si desea realizar modificaciones, haga clic **Atrás**; de lo contrario, haga clic en **Finalizar**.  
  
    > [!NOTE]  
    >  El Diseñador de cubos se puede usar cuando el Asistente para cubos haya completado la configuración del cubo. Además, puede usar el Diseñador de dimensiones para agregar, quitar y configurar atributos y jerarquías de las dimensiones que haya creado.  
  
  
