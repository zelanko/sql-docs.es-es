---
title: catalog.deploy_packages | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 8e861df6-d103-4d84-8438-e822533f6849
caps.latest.revision: "4"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a19a301fab52b0373eadb673d17e7436d0ffc1e2
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="catalogdeploypackages"></a>catalog.deploy_packages
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Implementa uno o más paquetes en una carpeta en el catálogo de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] o actualiza un paquete existente que se ha implementado previamente.  
  
## <a name="syntax"></a>Sintaxis  
  
```sql  
[catalog].[deploy_packages]     [ @folder_name = ] folder_name,    [ @project_name = ] project_name,    [ @packages_table = ] packages_table,     [ @operation_id OUTPUT ] operation_id OUTPUT ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @folder_name = ] *folder_name*  
 Nombre de la carpeta. *folder_name* es **nvarchar(128)**.  
  
 [ @project_name = ] *project_name*  
 Nombre del proyecto en la carpeta. *project_name* es **nvarchar(128)**.  
  
 [ @packages_table = ] *packages_table*  
 Contenido binario de archivos de paquete de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] (.dtsx). *packages_table* es **[catalog].[Package_Table_Type]**  
  
 [ @operation_id = ] *operation_id*  
 Devuelve el identificador único para la operación de implementación. *operation_id* es **bigint**.  
  
## <a name="return-code-value"></a>Valor de código de retorno  
 0 (correcto)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Ninguno  
  
## <a name="permissions"></a>Permissions  
 Este procedimiento almacenado necesita uno de los permisos siguientes:  
  
-   Permisos CREATE_OBJECTS en el proyecto o permisos MODIFY en el paquete para actualizar un paquete.  
  
-   Pertenencia al rol de base de datos **ssis_admin**  
  
-   Pertenencia al rol de servidor **sysadmin**  
  
## <a name="errors-and-warnings"></a>Errores y advertencias  
 La siguiente lista describe algunas condiciones que pueden hacer que este procedimiento almacenado produzca un error:  
  
-   Un parámetro hace referencia a un objeto que no existe, intenta crear un objeto que ya existe o no es válido por algún otro motivo.  
  
-   El usuario no tiene permisos suficientes  
  
  
