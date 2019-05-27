---
title: Asistente para importar proyectos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.importprojectwizard.f1
ms.assetid: 9247ad6c-4bd1-43ab-b347-583181cb9917
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: f1399b14ec9345b9ca312db463ba5e508d9b9bbe
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2019
ms.locfileid: "66058050"
---
# <a name="import-project-wizard"></a>Asistente para importar proyectos
  Use el Asistente para importar proyectos de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] para crear un nuevo proyecto de Integration Services a partir de otro existente. Se usa para importar proyectos que ya se han implementado en el catálogo de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] o para importar proyectos desde un archivo de implementación de proyecto (extensión .ispac).  
  
### <a name="to-create-a-project-based-on-a-project-in-ispac-file-or-in-catalog"></a>Para crear un proyecto basado en un proyecto del archivo .ispac o del catálogo  
  
1.  Haga clic en **Archivo**, seleccione **Nuevo**y haga clic en Proyecto.  
  
2.  Expanda **Business Intelligence**y haga clic en **Integration Services**.  
  
3.  Seleccione **Asistente para importación de Integration Services** en el panel central, escriba un **nombre** para el proyecto de solución, especifique la **carpeta** del proyecto y haga clic en **Aceptar**.  
  
     Debería aparecer el **Asistente para importar proyectos de Integration Services**. Este asistente crea un nuevo proyecto de Integration Services a partir de otro existente  
  
4.  Haga clic en **Siguiente** en la página **Introducción** para ver la página **Seleccionar origen** .  
  
5.  Especifique si desea importar el proyecto de un archivo .ispac o de un catálogo.  
  
    -   Si selecciona la opción **Archivo de implementación de proyecto** , especifique la ruta de acceso al archivo .ispac.  
  
    -   Si selecciona la opción **Catálogo de Integration Services** , especifique el nombre de la instancia de servidor de bases de datos en la que el catálogo existe, y la ruta de acceso al proyecto en el catálogo.  
  
6.  Haga clic en **Siguiente** en la página **Seleccionar origen** para ver la página **Revisar** . Revise la información mostrada en la página sobre la operación de importación que el asistente va a realizar.  
  
7.  Haga clic en **Importar** para crear un nuevo proyecto de Integration Services basado en el que ha seleccionado.  
  
8.  La página **Resultados** debe mostrar los resultados de la operación de importación que el asistente ha realizado. Haga clic en **Guardar informe** para guardar el informe en un archivo XML.  
  
9. Haga clic en **Cerrar** para cerrar el asistente.  
  
  
