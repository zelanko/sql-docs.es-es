---
title: 'Tarea 4: Crear un proyecto de SSIS con SQL Server Data Tools | Documentos de Microsoft'
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 8603ea91-2ec4-40b6-8070-4f824332f5d3
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 03c0a6599990357a255fab3beeb434db3cb5d97d
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36198076"
---
# <a name="task-4-creating-an-ssis-project-using-sql-server-data-tools"></a>Tarea 4: crear un proyecto de SSIS con SQL Server Data Tools
  En esta tarea, creará un proyecto de SSIS usando **SQL Server Data Tools** para automatizar la limpieza y la búsqueda de coincidencias de los datos de proveedor.  
  
1.  Inicie **SQL Server Data Tools**. Haga clic en Inicio, seleccione **Todos los programas**, expanda **Microsoft SQL Server 2012**y, a continuación, haga clic en **SQL Server Data Tools**.  
  
2.  En el menú **Archivo** , elija **Nuevo**y, a continuación, haga clic en **Proyecto**.  
  
3.  Expanda **Business Intelligence** en el panel **Plantillas instaladas** y seleccione **Integration Services**.  
  
     ![Visual Studio - cuadro de diálogo nuevo proyecto](../../2014/tutorials/media/et-creatinganssisprojectusingsqlsdt-01.jpg "Visual Studio - cuadro de diálogo nuevo proyecto")  
  
4.  Seleccione **Proyecto de Integration Services** en la **lista de tipos de proyecto**.  
  
5.  Escriba **CleanseAndCurateSuppliers** en **Nombre** y haga clic en **Aceptar**.  
  
6.  En la ventana **Explorador de soluciones** , haga clic con el botón secundario en **Package.dtsx** y seleccione **Cambiar nombre**. Si no ve la ventana **Explorador de soluciones** , haga clic en **Ver** en la barra de menús y, a continuación, haga clic en **Explorador de soluciones**.  
  
     ![Package.dtsx - menú renombrar](../../2014/tutorials/media/et-creatinganssisprojectusingsqlsdt-02.jpg "Package.dtsx - menú renombrar")  
  
7.  Escriba **CleanseAndCurate.dtsx** y presione **ENTRAR**. Asegúrese de que la **extensión** siga siendo **.dtsx**.  
  
## <a name="next-step"></a>Paso siguiente  
 [Tarea 5: Agregar una tarea de flujo de datos](task-5-adding-data-flow-task.md)  
  
  