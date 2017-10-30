---
title: Catalog.deploy_project (base de datos de SSISDB) | Documentos de Microsoft
ms.custom: 
ms.date: 03/09/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 2e3439b4-7226-4b61-a993-7a1d161eac7e
caps.latest.revision: 19
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: e20b96e38f798c19a74d5f3a32a25e429dc8ebeb
ms.openlocfilehash: 5682cd23cb65e097bccb8cc69d5f2ec88ece7709
ms.contentlocale: es-es
ms.lasthandoff: 10/20/2017

---
# <a name="catalogdeployproject-ssisdb-database"></a>catalog.deploy_project (base de datos de SSISDB)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Implementa un proyecto en una carpeta en el catálogo de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] o actualiza un proyecto existente que se ha implementado previamente.  
  
## <a name="syntax"></a>Sintaxis  
  
```sql  
catalog.deploy_project [@folder_name =] folder_name   
      , [@project_name =] project_name   
      , [@project_stream =] projectstream   
    [ , [@operation_id ] = operation_id OUTPUT ]   
```  
  
## <a name="arguments"></a>Argumentos  
 [@folder_name =] *nombreDeCarpeta*  
 El nombre de la carpeta donde se implementa el proyecto. El *nombre_de_carpeta* es **nvarchar (128)**.  
  
 [@project_name =] *Nombre_proyecto*  
 Nombre del proyecto nuevo o actualizado en la carpeta. El *Nombre_proyecto* es **nvarchar (128)**.  
  
 [@projectstream =] *projectstream*  
 Contenido binario de un archivo de implementación de proyecto (extensión .ispac) de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 Puede usar una instrucción SELECT con la función OPENROWSET y el proveedor de conjuntos de filas BULK para recuperar el contenido binario del archivo. Para obtener un ejemplo, vea [implementar Integration Services (SSIS) proyectos y paquetes](../../integration-services/packages/deploy-integration-services-ssis-projects-and-packages.md). Para obtener más información acerca de OPENROWSET, vea [OPENROWSET &#40; Transact-SQL &#41; ](../../t-sql/functions/openrowset-transact-sql.md).  
  
 El *projectstream* es **varbinary (max)**  
  
 [@operation_id =] *operation_id*  
 Devuelve el identificador único para la operación de implementación. El *operation_id* es **bigint**.  
  
## <a name="return-code-value"></a>Valor de código de retorno  
 0 (correcto)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Ninguno  
  
## <a name="permissions"></a>Permissions  
 Este procedimiento almacenado necesita uno de los permisos siguientes:  
  
-   Permisos CREATE_OBJECTS en la carpeta para implementar un nuevo proyecto o permisos MODIFY en el proyecto para actualizar un proyecto  
  
-   La pertenencia a la **ssis_admin** rol de base de datos  
  
-   La pertenencia a la **sysadmin** rol de servidor  
  
## <a name="errors-and-warnings"></a>Errores y advertencias  
 La siguiente lista describe algunas condiciones que pueden hacer que este procedimiento almacenado produzca un error:  
  
-   Un parámetro hace referencia a un objeto que no existe, un parámetro intenta crear un objeto que ya existe o un parámetro no es válido por algún otro motivo  
  
-   El valor del parámetro  *@project_name*  no coincide con el nombre del proyecto en el archivo de implementación  
  
-   El usuario no tiene permisos suficientes  
  
## <a name="remarks"></a>Comentarios  
 Durante la implementación o la actualización de un proyecto, el procedimiento almacenado no comprueba el nivel de protección de paquetes individuales en el proyecto.  
  
  

