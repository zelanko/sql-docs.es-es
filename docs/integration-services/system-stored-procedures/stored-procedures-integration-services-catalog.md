---
title: "(Catálogo de Integration Services) de procedimientos almacenados | Documentos de Microsoft"
ms.custom: 
ms.date: 12/16/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- stored procedures [Integration Services]
ms.assetid: a6ccd884-108f-4fb6-95ad-00b9cb65d5d6
caps.latest.revision: 19
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 21715bf65f3a85669dfe823511ddb9b6c2dd4d57
ms.contentlocale: es-es
ms.lasthandoff: 09/26/2017

---
# <a name="stored-procedures-integration-services-catalog"></a>Procedimientos almacenados (catálogo de Integration Services)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  En esta sección se describen los procedimientos almacenados de [!INCLUDE[tsql](../../includes/tsql-md.md)] disponibles para administrar proyectos de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] implementados en una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Llame a la [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] los procedimientos almacenados para agregar, quitar, modificar o ejecutar los objetos que se almacenan en la **SSISDB** catálogo.  
  
 El nombre predeterminado del catálogo es SSISDB. Entre los objetos que se almacenan en el catálogo se incluyen proyectos, paquetes, parámetros, entornos y el historial de operaciones.  
  
 Puede utilizar las vistas de base de datos y los procedimientos almacenados directamente, o escribir código personalizado que llame a la API administrada. [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] y la API administrada consultan las vistas y llaman a los procedimientos almacenados que se describen en esta sección para realizar muchas de sus tareas.  
  
## <a name="in-this-section"></a>En esta sección  
 [catalog.add_data_tap](../../integration-services/system-stored-procedures/catalog-add-data-tap.md)  
 Agrega una derivación de datos en la salida de un componente de un flujo de datos del paquete.  
  
 [catalog.add_data_tap_by_guid](../../integration-services/system-stored-procedures/catalog-add-data-tap-by-guid.md)  
 Agrega una derivación de datos a una ruta de flujo de datos específica en un flujo de datos del paquete.  
  
 [catalog.check_schema_version](../../integration-services/system-stored-procedures/catalog-check-schema-version.md)  
 Determina si el esquema del catálogo de SSISDB y los binarios de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] (ensamblado de ISServerExec y SQLCLR) son compatibles.  
  
 [Catalog.clear_object_parameter_value &#40; Base de datos SSISDB &#41;](../../integration-services/system-stored-procedures/catalog-clear-object-parameter-value-ssisdb-database.md)  
 Borra el valor de un parámetro para un paquete o proyecto de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] existente almacenado en el servidor.  
  
 [Catalog.configure_catalog &#40; Base de datos SSISDB &#41;](../../integration-services/system-stored-procedures/catalog-configure-catalog-ssisdb-database.md)  
 Configura el catálogo de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] estableciendo una propiedad de catálogo en un valor especificado.  
  
 [catalog.create_environment &#40;base de datos de SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-create-environment-ssisdb-database.md)  
 Crea un entorno en el catálogo de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 [catalog.create_environment_reference &#40;base de datos de SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-create-environment-reference-ssisdb-database.md)  
 Crea una referencia de entorno para un proyecto en el catálogo de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 [catalog.create_environment_variable &#40;base de datos de SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-create-environment-variable-ssisdb-database.md)  
 Cree una variable de entorno en el catálogo de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 [Catalog.create_execution &#40; Base de datos SSISDB &#41;](../../integration-services/system-stored-procedures/catalog-create-execution-ssisdb-database.md)  
 Crea una instancia de ejecución en el catálogo de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 [catalog.create_execution_dump](../../integration-services/system-stored-procedures/catalog-create-execution-dump.md)  
 Hace que un paquete en ejecución pause y cree un archivo de volcado.  
  
 [catalog.create_folder &#40;base de datos de SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-create-folder-ssisdb-database.md)  
 Crea una carpeta en el catálogo de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 [catalog.delete_environment &#40;base de datos de SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-delete-environment-ssisdb-database.md)  
 Elimina un entorno de una carpeta en el catálogo de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 [catalog.delete_environment_reference &#40;base de datos de SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-delete-environment-reference-ssisdb-database.md)  
 Elimina una referencia de entorno de un proyecto en el catálogo de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 [catalog.delete_environment_variable &#40;base de datos de SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-delete-environment-variable-ssisdb-database.md)  
 Elimina una variable de entorno de un entorno del catálogo de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 [catalog.delete_folder &#40;base de datos de SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-delete-folder-ssisdb-database.md)  
 Elimina una carpeta del catálogo de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 [catalog.delete_project &#40;base de datos de SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-delete-project-ssisdb-database.md)  
 Elimina un proyecto existente de una carpeta del catálogo de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 [Catalog.deny_permission &#40; Base de datos SSISDB &#41;](../../integration-services/system-stored-procedures/catalog-deny-permission-ssisdb-database.md)  
 Deniega un permiso en un objeto protegible del catálogo de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 [catalog.deploy_project &#40;base de datos de SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-deploy-project-ssisdb-database.md)  
 Implementa un proyecto en una carpeta en el catálogo de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] o actualiza un proyecto existente que se ha implementado previamente.  
  
 [Catalog.get_parameter_values &#40; Base de datos SSISDB &#41;](../../integration-services/system-stored-procedures/catalog-get-parameter-values-ssisdb-database.md)  
 Resuelve y recupera los valores de los parámetros predeterminados de un proyecto y los paquetes correspondientes en el catálogo de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 [catalog.get_project &#40;base de datos de SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-get-project-ssisdb-database.md)  
 Recupera las propiedades de un proyecto existente del catálogo de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 [Catalog.grant_permission &#40; Base de datos SSISDB &#41;](../../integration-services/system-stored-procedures/catalog-grant-permission-ssisdb-database.md)  
 Concede un permiso en un objeto protegible del catálogo de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 [catalog.move_environment &#40;base de datos de SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-move-environment-ssisdb-database.md)  
 Mueve un entorno desde una carpeta a otra en el catálogo de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 [catalog.move_project &#40;&#40;base de datos de SSISDB&#41;](../Topic/catalog.move_project%20\(\(SSISDB%20Database\).md)  
 Mueve un proyecto desde una carpeta a otra del catálogo de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 [catalog.remove_data_tap](../../integration-services/system-stored-procedures/catalog-remove-data-tap.md)  
 Quita una derivación de datos de la salida de un componente que está en una ejecución.  
  
 [catalog.rename_environment &#40;base de datos de SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-rename-environment-ssisdb-database.md)  
 Cambia el nombre de un entorno en el catálogo de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 [catalog.rename_folder &#40;base de datos de SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-rename-folder-ssisdb-database.md)  
 Cambia el nombre de una carpeta en el catálogo de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 [catalog.restore_project &#40;base de datos de SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-restore-project-ssisdb-database.md)  
 Restaura un proyecto del catálogo de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] a una versión anterior.  
  
 [Catalog.revoke_permission &#40; Base de datos SSISDB &#41;](../../integration-services/system-stored-procedures/catalog-revoke-permission-ssisdb-database.md)  
 Revoca un permiso de un objeto protegible en el catálogo de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 [catalog.set_environment_property &#40;base de datos de SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-set-environment-property-ssisdb-database.md)  
 Establece la propiedad de un entorno del catálogo de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 [catalog.set_environment_reference_type &#40;base de datos de SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-set-environment-reference-type-ssisdb-database.md)  
 Establece el tipo de referencia y el nombre del entorno asociados con una referencia de entorno existente para un proyecto en el catálogo de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 [catalog.set_environment_variable_property &#40;base de datos de SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-set-environment-variable-property-ssisdb-database.md)  
 Establece la propiedad de una variable de entorno en el catálogo de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 [Catalog.set_environment_variable_protection &#40; Base de datos SSISDB &#41;](../../integration-services/system-stored-procedures/catalog-set-environment-variable-protection-ssisdb-database.md)  
 Establece el bit de sensibilidad de una variable de entorno en el catálogo [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 [catalog.set_environment_variable_value &#40;base de datos de SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-set-environment-variable-value-ssisdb-database.md)  
 Establece el valor de una variable de entorno en el catálogo de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 [catalog.set_execution_parameter_value &#40;base de datos de SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database.md)  
 Establece el valor de un parámetro para una instancia de ejecución en el catálogo [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 [catalog.set_execution_property_override_value](../../integration-services/system-stored-procedures/catalog-set-execution-property-override-value.md)  
 Establece el valor de una propiedad para una instancia de ejecución en el catálogo de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 [catalog.set_folder_description &#40;base de datos de SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-set-folder-description-ssisdb-database.md)  
 Establece la descripción de una carpeta en el catálogo de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 [Catalog.set_object_parameter_value &#40; Base de datos SSISDB &#41;](../../integration-services/system-stored-procedures/catalog-set-object-parameter-value-ssisdb-database.md)  
 Establece el valor de un parámetro del catálogo de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Asocia el valor a una variable de entorno o asigna un valor literal que se va a usar como valor predeterminado si no se asignan otros valores.  
  
 [Catalog.start_execution &#40; Base de datos SSISDB &#41;](../../integration-services/system-stored-procedures/catalog-start-execution-ssisdb-database.md)  
 Inicia una instancia de ejecución en el catálogo de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 [catalog.startup](../../integration-services/system-stored-procedures/catalog-startup.md)  
 Realiza el mantenimiento del estado de las operaciones del catálogo de SSISDB.  
  
 [Catalog.stop_operation &#40; Base de datos SSISDB &#41;](../../integration-services/system-stored-procedures/catalog-stop-operation-ssisdb-database.md)  
 Detiene una validación o instancia de ejecución en el catálogo de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 [Catalog.validate_package &#40; Base de datos SSISDB &#41;](../../integration-services/system-stored-procedures/catalog-validate-package-ssisdb-database.md)  
 Valida de forma asincrónica un paquete del catálogo de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 [Catalog.validate_project &#40; Base de datos SSISDB &#41;](../../integration-services/system-stored-procedures/catalog-validate-project-ssisdb-database.md)  
 Valida de forma asincrónica un proyecto del catálogo de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
[Catalog.add_execution_worker &#40; Base de datos SSISDB &#41;](../../integration-services/system-stored-procedures/catalog-add-execution-worker-ssisdb-database.md)   
Agrega un [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] escala Out trabajador a una instancia de ejecución en horizontalmente.

[Catalog.enable_worker_agent &#40; Base de datos SSISDB &#41;](../../integration-services/system-stored-procedures/catalog-enable-worker-agent-ssisdb-database.md)   
Habilitar un trabajo de salida de escala para trabajan con esta escala Out Master [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] catálogo.

[Catalog.disable_worker_agent &#40; Base de datos SSISDB &#41;](../../integration-services/system-stored-procedures/catalog-disable-worker-agent-ssisdb-database.md)   
Deshabilitar un trabajo de salida de escala para trabajar con esta escala Out maestro [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] catálogo.



