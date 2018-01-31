---
title: catalog.configure_catalog (base de datos de SSISDB) | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 72690c61-f462-4c25-9fce-08a687b0bd41
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6d1f8926d398a90214a5ad1903f04ac1e29d8854
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/25/2018
---
# <a name="catalogconfigurecatalog-ssisdb-database"></a>catalog.configure_catalog (base de datos de SSISDB)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Configura el catálogo de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] estableciendo una propiedad de catálogo en un valor especificado.  
  
## <a name="syntax"></a>Sintaxis  
  
```sql
catalog.configure_catalog [ @property_name = ] property_name , [ @property_value = ] property_value  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @property_name = ] *property_name*  
 Nombre de la propiedad de catálogo. *property_name* es **nvarchar(255)**. Para obtener más información sobre las propiedades disponibles, vea [catalog.catalog_properties &#40; Base de datos SSISDB &#41;](../../integration-services/system-views/catalog-catalog-properties-ssisdb-database.md).  
  
 [ @property_value = ] *property_value*  
 Valor de la propiedad de catálogo. *property_value* es **nvarchar(255)**. Para obtener más información sobre los valores de las propiedades, vea [catalog.catalog_properties &#40; Base de datos SSISDB &#41;](../../integration-services/system-views/catalog-catalog-properties-ssisdb-database.md).  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 None  
  
## <a name="remarks"></a>Notas  
 Este procedimiento almacenado determina si *property_value* es válido para cada *property_name*.  
  
 Este procedimiento almacenado solo se puede realizar cuando no hay ninguna ejecución activa, como ejecuciones pendientes, en cola, en ejecución y en pausa.  
  
 Mientras se está configurando el catálogo, todos los demás procedimientos almacenados de catálogo producirán un error y mostrarán el mensaje de error "El servidor se está configurando actualmente".
  
 Cuando el catálogo está configurado, se escribe una entrada en el registro de operaciones.  
  
## <a name="permissions"></a>Permisos  
 Este procedimiento almacenado necesita uno de los permisos siguientes:  
  
-   Pertenencia al rol de base de datos de **ssis_admin**  
  
-   Pertenencia al rol de servidor de **sysadmin**  
  
## <a name="errors-and-warnings"></a>Errores y advertencias  
 En la siguiente lista se describen algunas condiciones que pueden producir un error o una advertencia:  
  
-   La propiedad no existe  
  
-   El valor de la propiedad no es válido  
  
  
