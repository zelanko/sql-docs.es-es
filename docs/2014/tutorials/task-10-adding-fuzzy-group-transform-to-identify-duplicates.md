---
title: 'Tarea 10: agregar una transformación agrupación aproximada para identificar duplicados | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 90b2b323-babd-464a-8914-9dc5e66aca74
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: e7091c4dbb8244476357afba18e973535def8baa
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85064810"
---
# <a name="task-10-adding-fuzzy-group-transform-to-identify-duplicates"></a>Tarea 10: Adición de la transformación Agrupación aproximada para identificar duplicados
  En esta tarea, agregará una transformación Agrupación aproximada al flujo de datos. La transformación Agrupación aproximada puede ayudar a identificar duplicados en los datos de origen. Vea [transformación agrupación aproximada](../integration-services/data-flow/transformations/fuzzy-grouping-transformation.md) para obtener más detalles.  
  
1.  Arrastre y coloque la transformación **agrupación aproximada** en **otras transformaciones** del **cuadro de herramientas de SSIS** en la pestaña flujo de **datos** en **combinar registros correctos y corregidos**.  
  
2.  Haga clic con el botón secundario en transformación **agrupación aproximada** en la pestaña **flujo de datos** y haga clic en **cambiar nombre**. Escriba **grupos de proveedores con identificadores coincidentes** y presione **entrar**.  
  
3.  Conecte **combinar registros correctos y corregidos** para **agrupar proveedores con ID. coincidentes** mediante el conector azul.  
  
     ![Conexión a grupos de proveedores con Id. coincidentes](../../2014/tutorials/media/et-addingfgttoidentifyduplicates-01.jpg "Conexión a grupos de proveedores con Id. coincidentes")  
  
4.  Haga doble clic en **agrupar proveedores con identificadores coincidentes**.  
  
5.  En el **Editor de transformación agrupación aproximada**, haga clic en **nuevo** junto a **OLE DB lista** desplegable administrador de conexiones para abrir el cuadro de diálogo **configurar el administrador de conexiones OLE DB** .  
  
6.  En el cuadro de diálogo, haga clic en **nuevo** para iniciar el cuadro de diálogo **Administrador de conexiones** .  
  
7.  Escriba **(local)** o **punto** (.) como nombre del servidor.  
  
8.  Seleccione **MDS** para **Seleccione o escriba un** campo de nombre de base de datos. Usará la base de datos de MDS como almacenamiento temporal para la **transformación agrupación aproximada**. La transformación **agrupación aproximada** requiere una conexión a una instancia de SQL Server para crear las tablas temporales de SQL Server que requiere el algoritmo de transformación para realizar su trabajo. Puede crear una base de datos o usar otra base de datos existente con este fin.  
  
9. Haga clic en **probar conexión** para probar la conexión y haga clic en **Aceptar** en el cuadro de mensaje.  
  
10. En el cuadro de diálogo **Administrador de conexiones** , haga clic en **Aceptar**.  
  
11. Seleccione **(local). MDS** (o **localhost). MDS**) de la **lista de conexiones de datos** y haga clic en **Aceptar**.  
  
12. En el **Editor de transformación agrupación aproximada**, confirme que **(local). MDS** o **localhost. MDS** está seleccionado para el **Administrador de conexiones de OLE DB**.  
  
13. Cambie a la pestaña **columnas** .  
  
14. Active (casilla) **SupplierID_Output** de la lista de **columnas de entrada disponibles**. Para configurar la transformación, seleccione las columnas de entrada que se usarán al identificar duplicados. Por simplificar, use solo la columna SupplierID en este paso.  
  
     ![Agrupación aproximada, editor de transformación](../../2014/tutorials/media/et-addingfgttoidentifyduplicates-02.jpg "Agrupación aproximada, editor de transformación")  
  
15. Haga clic en **Aceptar** para cerrar el **Editor de transformación agrupación aproximada**.  
  
## <a name="next-step"></a>siguiente paso  
 [Tarea 11: Adición de la transformación División condicional para filtrar duplicados](../../2014/tutorials/task-11-adding-conditional-split-transform-to-filter-duplicates.md)  
  
  
