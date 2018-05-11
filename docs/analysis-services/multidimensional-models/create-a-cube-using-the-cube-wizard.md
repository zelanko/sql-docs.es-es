---
title: Crear un cubo con el Asistente para cubos | Documentos de Microsoft
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 64083ec89d9d606c5c5a942bc45b09259c49e023
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="create-a-cube-using-the-cube-wizard"></a>Crear un cubo con el Asistente para cubos
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
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
  
  
