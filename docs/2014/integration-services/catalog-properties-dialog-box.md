---
title: Cuadro de diálogo Propiedades del catálogo | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.ssms.iscatalogprop.general.f1
- sql12.ssis.ssms.iscreatecatalog.f1
ms.assetid: 3e2fcf11-e010-41c6-bc26-e4b281c0bfbc
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 8d3492cce19906322ef9b420718aae0ae9e0e62d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66061112"
---
# <a name="catalog-properties-dialog-box"></a>Propiedades del catálogo, cuadro de diálogo
  Utilice el cuadro de diálogo Propiedades del catálogo para configurar el catálogo de SSISDB. Las propiedades del catálogo definen cómo se cifra la información confidencial, cómo se conservan las operaciones y los datos de control de versiones del proyecto, y cuándo se agota el tiempo de espera de las operaciones de validación. El catálogo de SSISDB es un punto de administración y almacenamiento [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] central para proyectos, paquetes, parámetros y entornos.  
  
 También puede ver las propiedades del catálogo en la vista catalog.catalog_property y establecer las propiedades utilizando el procedimiento almacenado catalog.configure_catalog. Para más información, vea [catalog.catalog_properties &#40;base de datos SSISDB&#41;](/sql/integration-services/system-views/catalog-catalog-properties-ssisdb-database) y [catalog.configure_catalog &#40;base de datos SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-configure-catalog-ssisdb-database).  
  
 Para más información sobre cómo crear el catálogo de SSISDB, vea [Crear el catálogo de SSIS](catalog/ssis-catalog.md).  
  
 **¿Qué desea hacer?**  
  
-   [Abrir el cuadro de diálogo Propiedades del catálogo](#open_dialog)  
  
-   [Configurar las opciones](#options)  
  
##  <a name="open_dialog"></a>Abrir el cuadro de diálogo Propiedades del catálogo  
  
1.  Abra [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)][!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)].  
  
2.  Conéctese al motor de base de datos de Microsoft SQL Server.  
  
3.  En el Explorador de objetos, expanda el nodo **Integration Services** , haga clic con el botón derecho en **SSISDB**y luego haga clic en **Propiedades**.  
  
##  <a name="options"></a> Configurar las opciones  
  
### <a name="options"></a>Opciones  
 En la tabla siguiente se describen algunas propiedades del cuadro de diálogo y las propiedades correspondientes de la vista catalog.catalog_property.  
  
|Nombre de la propiedad (cuadro de diálogo Propiedades del catálogo)|Nombre de la propiedad (vista catalog.catalog_property).|Descripción|  
|-----------------------------------------------------|------------------------------------------------------|-----------------|  
|Nombre del algoritmo de cifrado|ENCRYPTION_CLEANUP_ENABLED|Especifica el tipo de cifrado que se utiliza para cifrar los valores de los parámetros confidenciales del catálogo. Los posibles valores son los siguientes:<br /><br /> **DES**<br /><br /> **TRIPLE_DES**<br /><br /> **TRIPLE_DES_3KEY**<br /><br /> **DESPX**<br /><br /> **AES_128**<br /><br /> **AES_192**<br /><br /> **AES_256** (valor predeterminado)|  
|Tiempo de espera de validación (segundos)|VALIDATION_TIMEOUT|Especifica el número de máximo de segundos que puede ejecutarse la validación de un proyecto o de un paquete antes de que se detenga. El valor predeterminado es 300 segundos.<br /><br /> La validación es una operación asincrónica. Cuanto mayor sea el proyecto o el paquete, más se tardará en validar.<br /><br /> Para obtener información sobre la validación de proyectos y paquetes, vea [Integration Services Data Types in Expressions](expressions/integration-services-data-types-in-expressions.md).|  
|Borrar registros periódicamente|OPERATION_CLEANUP_ENABLED|Establezca la propiedad en True para indicar que se ejecuta el trabajo limpieza de operaciones del Agente SQL Server. En caso contrario, establezca la propiedad en False.|  
|Período de retención (días)|RETENTION_WINDOW|Especifique la antigüedad máxima de los datos permitidos para las operaciones (en días). El trabajo limpieza de operaciones del Agente SQL Server quitará los datos anteriores al número de días especificado.|  
|Número máximo de versiones por proyecto|MAX_PROJECT_VERSIONS|Especifique cuántas versiones de un proyecto se almacenarán en el catálogo. Las versiones anteriores de los proyectos que superen el máximo se quitarán cuando se ejecute el trabajo de limpieza de versiones del proyecto.|  
  
  
