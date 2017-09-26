---
title: Catalog.configure_catalog (base de datos de SSISDB) | Documentos de Microsoft
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 72690c61-f462-4c25-9fce-08a687b0bd41
caps.latest.revision: 13
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: c9e285e62e2b391939d8811b5a194a12ad55636d
ms.contentlocale: es-es
ms.lasthandoff: 09/26/2017

---
# <a name="catalogconfigurecatalog-ssisdb-database"></a>catalog.configure_catalog (base de datos de SSISDB)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Configura el catálogo de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] estableciendo una propiedad de catálogo en un valor especificado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
configure_catalog [ @property_name = ] property_name , [ @property_value = ] property_value  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @property_name =] *property_name*  
 Nombre de la propiedad de catálogo. El *property_name* es **nvarchar (255)**. Para obtener más información sobre las propiedades disponibles, vea [catalog.catalog_properties &#40; Base de datos SSISDB &#41; ](../../integration-services/system-views/catalog-catalog-properties-ssisdb-database.md).  
  
 [ @property_value =] *property_value*  
 Valor de la propiedad de catálogo. El *property_value* es **nvarchar (255)**. Para obtener más información acerca de los valores de propiedad, vea [catalog.catalog_properties &#40; Base de datos SSISDB &#41;](../../integration-services/system-views/catalog-catalog-properties-ssisdb-database.md)  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Ninguno  
  
## <a name="remarks"></a>Comentarios  
 Este procedimiento almacenado determina si el *property_value* es válido para cada *property_name*.  
  
 Este procedimiento almacenado solo se puede realizar cuando no hay ninguna ejecución activa, como ejecuciones pendientes, en cola, en ejecución y en pausa.  
  
 Mientras se está configurando el catálogo, todos los otros catálogos almacenan procedimientos producirá un error con el mensaje de error "Servidor se está configurando actualmente".  
  
 Cuando el catálogo está configurado, se escribe una entrada en el registro de operaciones.  
  
## <a name="permissions"></a>Permissions  
 Este procedimiento almacenado necesita uno de los permisos siguientes:  
  
-   La pertenencia a la **ssis_admin** rol de base de datos  
  
-   La pertenencia a la **sysadmin** rol de servidor  
  
## <a name="errors-and-warnings"></a>Errores y advertencias  
 En la siguiente lista se describen algunas condiciones que pueden producir un error o una advertencia:  
  
-   La propiedad no existe  
  
-   El valor de la propiedad no es válido  
  
  
