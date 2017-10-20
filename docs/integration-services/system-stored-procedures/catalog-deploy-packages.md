---
title: Catalog.deploy_packages | Documentos de Microsoft
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 8e861df6-d103-4d84-8438-e822533f6849
caps.latest.revision: 4
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 1839430dd7fb83ab16c4de46011819e3ce28e835
ms.contentlocale: es-es
ms.lasthandoff: 09/26/2017

---
# <a name="catalogdeploypackages"></a>Catalog.deploy_packages
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Implementa uno o varios paquetes en una carpeta en el [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] de catálogo o actualiza un paquete existente que se ha implementado previamente.  
  
## <a name="syntax"></a>Sintaxis  
  
```sql  
[catalog].[deploy_packages]     [ @folder_name = ] folder_name,    [ @project_name = ] project_name,    [ @packages_table = ] packages_table,     [ @operation_id OUTPUT ] operation_id OUTPUT ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @folder_name =] *nombreDeCarpeta*  
 Nombre de la carpeta. El *nombre_de_carpeta* es **nvarchar (128)**.  
  
 [ @project_name =] *Nombre_proyecto*  
 El nombre del proyecto en la carpeta. El *Nombre_proyecto* es **nvarchar (128)**.  
  
 [ @packages_table =] *packages_table*  
 El contenido binario de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] (.dtsx) archivos del paquete. El *packages_table* es **[catalog]. [ Package_Table_Type]**  
  
 [ @operation_id =] *operation_id*  
 Devuelve el identificador único para la operación de implementación. El *operation_id* es **bigint**.  
  
## <a name="return-code-value"></a>Valor de código de retorno  
 0 (correcto)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Ninguno  
  
## <a name="permissions"></a>Permissions  
 Este procedimiento almacenado necesita uno de los permisos siguientes:  
  
-   Permisos CREATE_OBJECTS en el proyecto o los permisos de modificación en el paquete para actualizar un paquete.  
  
-   La pertenencia a la **ssis_admin** rol de base de datos  
  
-   La pertenencia a la **sysadmin** rol de servidor  
  
## <a name="errors-and-warnings"></a>Errores y advertencias  
 La siguiente lista describe algunas condiciones que pueden hacer que este procedimiento almacenado produzca un error:  
  
-   Un parámetro hace referencia a un objeto que no existe, intente crear un objeto que ya existe un parámetro o un parámetro no es válido en alguna otra manera.  
  
-   El usuario no tiene permisos suficientes  
  
  
