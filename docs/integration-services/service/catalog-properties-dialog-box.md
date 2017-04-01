---
title: "Propiedades del cat&#225;logo, cuadro de di&#225;logo | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.ssis.ssms.iscreatecatalog.f1"
  - "sql13.ssis.ssms.iscatalogprop.general.f1"
ms.assetid: 3e2fcf11-e010-41c6-bc26-e4b281c0bfbc
caps.latest.revision: 8
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 8
---
# Propiedades del cat&#225;logo, cuadro de di&#225;logo
  Utilice el cuadro de diálogo Propiedades del catálogo para configurar el catálogo de SSISDB. Las propiedades del catálogo definen cómo se cifra la información confidencial, cómo se conservan las operaciones y los datos de versiones del proyecto, y el tiempo de espera de las operaciones de validación. El catálogo de SSISDB es un punto centralizado de almacenamiento y administración para los proyectos, paquetes, parámetros y entornos de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
 También puede ver las propiedades del catálogo en la vista catalog.catalog_property y establecer las propiedades utilizando el procedimiento almacenado catalog.configure_catalog. Para más información, vea [catalog.catalog_properties &#40;base de datos SSISDB&#41;](../../integration-services/system-views/catalog-catalog-properties-ssisdb-database.md) y [catalog.configure_catalog &#40;base de datos SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-configure-catalog-ssisdb-database.md).  
  
 Para más información sobre cómo crear el catálogo de SSISDB, vea [Crear el catálogo de SSIS](../../integration-services/service/create-the-ssis-catalog.md).  
  
 **¿Qué desea hacer?**  
  
-   [Abrir el cuadro de diálogo Propiedades del catálogo](#open_dialog)  
  
-   [Configurar las opciones](#options)  
  
##  <a name="open_dialog"></a> Abrir el cuadro de diálogo Propiedades del catálogo  
  
1.  Abra [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].  
  
2.  Conéctese al motor de base de datos de Microsoft SQL Server.  
  
3.  En el Explorador de objetos, expanda el nodo **Integration Services**, haga clic con el botón derecho en **SSISDB** y luego haga clic en **Propiedades**.  
  
##  <a name="options"></a> Configurar las opciones  
  
### Opciones  
 En la tabla siguiente se describen algunas propiedades del cuadro de diálogo y las propiedades correspondientes de la vista catalog.catalog_property.  
  
|Nombre de la propiedad (cuadro de diálogo Propiedades del catálogo)|Nombre de la propiedad (vista catalog.catalog_property).|Description|  
|-----------------------------------------------------|------------------------------------------------------|-----------------|  
|Nombre del algoritmo de cifrado|ENCRYPTION_CLEANUP_ENABLED|Especifica el tipo de cifrado que se utiliza para cifrar los valores de los parámetros confidenciales del catálogo. Los posibles valores son los siguientes:<br /><br /> DES<br /><br /> TRIPLE_DES<br /><br /> TRIPLE_DES_3KEY<br /><br /> DESPX<br /><br /> AES_128<br /><br /> AES_192<br /><br /> AES_256 (predeterminado)|  
|Tiempo de espera de validación (segundos)|VALIDATION_TIMEOUT|Especifica el número de máximo de segundos que puede ejecutarse la validación de un proyecto o de un paquete antes de que se detenga. El valor predeterminado es 300 segundos.<br /><br /> La validación es una operación asincrónica. Cuanto mayor sea el proyecto o el paquete, más se tardará en validar.<br /><br /> Para obtener información sobre la validación de proyectos y paquetes, vea [Integration Services Data Types in Expressions](../../integration-services/expressions/integration-services-data-types-in-expressions.md).|  
|Borrar registros periódicamente|OPERATION_CLEANUP_ENABLED|Establezca la propiedad en True para indicar que se ejecuta el trabajo limpieza de operaciones del Agente SQL Server. En caso contrario, establezca la propiedad en False.|  
|Período de retención (días)|RETENTION_WINDOW|Especifique la antigüedad máxima de los datos permitidos para las operaciones (en días). El trabajo limpieza de operaciones del Agente SQL Server quitará los datos anteriores al número de días especificado.|  
|Número máximo de versiones por proyecto|MAX_PROJECT_VERSIONS|Especifique cuántas versiones de un proyecto se almacenarán en el catálogo. Las versiones anteriores de los proyectos que superen el máximo se quitarán cuando se ejecute el trabajo de limpieza de versiones del proyecto.|  
  
  