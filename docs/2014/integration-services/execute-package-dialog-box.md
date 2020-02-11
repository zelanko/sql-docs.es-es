---
title: Cuadro de diálogo Ejecutar paquete | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.ssms.ispackageexecute.f1
- sql12.ssis.ssms.executepackage.f1
ms.assetid: 4f7a806d-4867-4d1f-bc65-b00c1caee7b6
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: b4b920b17e960059e1212be7dd15c176c0b25a47
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66059185"
---
# <a name="execute-package-dialog-box"></a>Execute Package Dialog Box
  Use el cuadro de diálogo **Ejecutar paquete** para ejecutar un paquete que está almacenado en el servidor de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] .  
  
 Un paquete de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] puede contener parámetros que hagan referencia a valores almacenados en variables de entorno. Antes de ejecutar este tipo de paquete, debe especificar qué referencia del entorno se utilizará para proporcionar los valores de la variable de entorno. Un proyecto puede contener varios entornos, pero se puede utilizar solo un entorno para enlazar los valores de variable de entorno en el momento de la ejecución. Si no se usan variables de entorno en el paquete, no se requiere un entorno.  
  
 ¿Qué desea hacer?  
  
-   [Abrir el cuadro de diálogo Ejecutar paquete](#open_dialog)  
  
-   [Establecer las opciones de la página general](#general)  
  
-   [Establecer las opciones de la pestaña parámetros](#parameters)  
  
-   [Establecer las opciones de la pestaña administradores de conexiones](#connection)  
  
-   [Establecer las opciones de la pestaña Opciones avanzadas](#advanced)  
  
-   [Scripting de las opciones del cuadro de diálogo Ejecutar paquete](#script)  
  
##  <a name="open_dialog"></a>Abrir el cuadro de diálogo Ejecutar paquete  
  
1.  En [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], conéctese al servidor de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] .  
  
     Se conectará a la instancia del [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] que hospeda la base de datos SSISDB.  
  
2.  En el Explorador de objetos, expanda el árbol para que se muestre el nodo **Catálogos de Integration Services** .  
  
3.  Expanda el nodo **SSISDB** .  
  
4.  Expanda la carpeta que contiene el paquete que desea ejecutar.  
  
5.  Haga clic con el botón derecho en el paquete y, después, haga clic en **Ejecutar**.  
  
##  <a name="general"></a>Establecer las opciones de la página general  
 Seleccione **Entorno** para especificar el entorno que se aplica cuando se ejecuta el paquete.  
  
##  <a name="parameters"></a>Establecer las opciones de la pestaña parámetros  
 Utilice la pestaña **Parámetros** para modificar los valores de parámetro que se utilizan cuando se ejecuta el paquete.  
  
##  <a name="connection"></a>Establecer las opciones de la pestaña administradores de conexiones  
 Utilice la pestaña Administradores de conexiones para establecer las propiedades de los administradores de conexiones del paquete.  
  
##  <a name="advanced"></a>Establecer las opciones de la pestaña Opciones avanzadas  
 Utilice la pestaña Avanzadas para administrar propiedades y otra configuración del paquete.  
  
 **Agregar**, **Editar**, **quitar**  
 Haga clic para agregar, editar o quitar una propiedad.  
  
 **Nivel de registro**  
 Seleccione el nivel de registro de la ejecución del paquete. Para más información, vea [catalog.set_execution_parameter_value &#40;base de datos de SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database).  
  
 **Volcado de errores**  
 Especifique si se crea un archivo de volcado cuando se producen errores durante la ejecución del paquete. Para obtener más información, consulte [Generating Dump Files for Package Execution](troubleshooting/generating-dump-files-for-package-execution.md).  
  
 **tiempo de ejecución de 32 bits**  
 Especifique que el paquete se ejecutará en un sistema de 32 bits.  
  
##  <a name="script"></a>Scripting de las opciones del cuadro de diálogo Ejecutar paquete  
 Mientras está en el cuadro de diálogo **Ejecutar paquete** , también puede utilizar el botón **Script** de la barra de herramientas para escribir código de [!INCLUDE[tsql](../includes/tsql-md.md)] . El script generado realiza una llamada a los procedimientos almacenados [catalog.start_execution &#40;base de datos de SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-start-execution-ssisdb-database) con las mismas opciones que ha seleccionado en el cuadro de diálogo **Ejecutar paquete**. El script aparece en una nueva ventana de script en [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)].  
  
  
