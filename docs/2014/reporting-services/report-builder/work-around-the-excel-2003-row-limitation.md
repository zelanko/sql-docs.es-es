---
title: Evitar la limitación de filas de Excel | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: a4c8700b-bef5-4440-a99c-bba5dcc46bfd
caps.latest.revision: 6
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 041872122516c411e7b02b7dde85c248600904cc
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37260471"
---
# <a name="work-around-the-excel-row-limitation"></a>Solución alternativa de la limitación de filas de Excel
  En este tema se explica cómo resolver la limitación de filas de Excel 2003 al exportar informes a Excel. La solución alternativa es para un informe que solo contiene una tabla.  
  
 Excel 2003 admite un máximo de 65.536 filas por hoja de cálculo. Puede evitar esta limitación si fuerza un salto de página explícito después de un número determinado de filas. El representador de Excel crea una nueva hoja de cálculo por cada salto de página explícito.  
  
### <a name="to-create-an-explicit-page-break"></a>Para crear un salto de página explícito  
  
1.  Abra el informe en [!INCLUDE[ss_dtbi](../../includes/ss-dtbi-md.md)] o en el Administrador de informes.  
  
2.  Haga clic con el botón derecho en la fila Datos de la tabla y, después, haga clic en **Agregar grupo** > **Grupo primario** para agregar un grupo de tablas externo.  
  
     ![Seleccionar el grupo primario](../media/datarow-selectparentgroup.png "Seleccionar el grupo primario")  
  
3.  Escriba la fórmula siguiente en el cuadro de expresión **Agrupar por** y, a continuación, haga clic en **Aceptar** para agregar el grupo primario.  
  
     =Int((RowNumber(Nothing)-1)/65000)  
  
     La fórmula asigna un número a cada conjunto de 65000 filas del conjunto de datos. Cuando se define un salto de página para el grupo, la expresión produce un salto de página cada 65000 filas.  
  
     Al agregar el grupo de tablas exterior agrega una columna de grupo al informe.  
  
4.  Elimine la columna de grupo; para ello, haga clic con el botón derecho en el encabezado de columna, haga clic en **Eliminar columnas**, seleccione **Eliminar solo columnas**y, después, haga clic en **Aceptar**.  
  
     ![Eliminar un grupo de columnas](../media/groupcolumn-delete-updated.png "Eliminar un grupo de columnas")  
  
5.  Haga clic con el botón secundario en **Grupo 1** en la sección **Grupos de filas** y, a continuación, haga clic en **Propiedades de grupo**.  
  
     ![Ver propiedades de grupo](../media/groupproperties-updated.png "Ver propiedades de grupo")  
  
6.  En la página **Ordenación** del cuadro de diálogo **Propiedades de grupo** , seleccione la opción de ordenación predeterminada y haga clic en **Eliminar**.  
  
     ![Eliminar la ordenación predeterminada](../media/groupproperties-sorting-updated.png "Eliminar la ordenación predeterminada")  
  
7.  En la página **Saltos de página** , haga clic en **Entre cada instancia de un grupo** y, a continuación, haga clic en **Aceptar**.  
  
     ![Establecer saltos de página](../media/groupproperties-pagebreaks-updated.png "Establecer saltos de página")  
  
8.  Guarde el informe. Cuando lo exporta a Excel, se exporta a varias hojas de cálculo y cada hoja de cálculo contiene un máximo de 65000 filas.  
  
  
