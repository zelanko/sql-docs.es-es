---
description: catalog.check_schema_version
title: catalog.check_schema_version | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: e0d5e9f5-59c6-4118-87b5-4aa5c37a7df6
author: chugugrace
ms.author: chugu
ms.openlocfilehash: b8f1d04f2a41c247a3de8a66f5b07ee74f5036b5
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/25/2020
ms.locfileid: "96129945"
---
# <a name="catalogcheck_schema_version"></a>catalog.check_schema_version 

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Determina si el esquema del catálogo de SSISDB y los binarios de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] (ensamblado de ISServerExec y SQLCLR) son compatibles.  
  
 ISServerExec.exc registra un mensaje de error cuando el esquema y los archivos binarios son incompatibles.  
  
 La versión de esquema de SSISDB aumenta cuando el esquema se modifica durante la aplicación de revisiones y durante las actualizaciones. Se recomienda ejecutar este procedimiento almacenado después haber restaurado una copia de seguridad de SSISDB para asegurarse de que el esquema y los archivos binarios son compatibles.  
  
## <a name="syntax"></a>Sintaxis  
  
```sql  
catalog.check_schema_version [ @use32bitruntime = ] use32bitruntime  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @use32bitruntime= ] *use32bitruntime*  
 Cuando el parámetro se establece en **1**, se llama a la versión de 32 bits de dtexec. *use32bitruntime* es de tipo **int**.  
  
## <a name="result-set"></a>Tipo de cursor  
 None  
  
## <a name="permissions"></a>Permisos  
 Este procedimiento almacenado necesita el siguiente permiso:  
  
-   Pertenencia al rol de base de datos de **ssis_admin**  
  
  
