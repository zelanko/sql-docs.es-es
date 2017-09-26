---
title: Catalog.check_schema_version | Documentos de Microsoft
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: e0d5e9f5-59c6-4118-87b5-4aa5c37a7df6
caps.latest.revision: 5
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 56eacb6ed209f34f65ae406fe4dd520284b79e5b
ms.contentlocale: es-es
ms.lasthandoff: 09/26/2017

---
# <a name="catalogcheckschemaversion"></a>catalog.check_schema_version
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Determina si el esquema del catálogo de SSISDB y los binarios de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] (ensamblado de ISServerExec y SQLCLR) son compatibles.  
  
 ISServerExec.exc registra un mensaje de error cuando el esquema y los archivos binarios son incompatibles.  
  
 La versión de esquema de SSISDB aumenta cuando el esquema se modifica durante la aplicación de revisiones y durante las actualizaciones. Se recomienda ejecutar este procedimiento almacenado después haber restaurado una copia de seguridad de SSISDB para asegurarse de que el esquema y los archivos binarios son compatibles.  
  
## <a name="syntax"></a>Sintaxis  
  
```vb  
Check_schema_version [@use32bitruntime = ] use32bitruntime  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @use32bitruntime=] *use32bitruntime*  
 Cuando el parámetro se establece en **True**, se llama a la versión de 32 bits de dtexec. El *use32bitruntime* es un **Bool**.  
  
## <a name="result-set"></a>Conjunto de resultados  
 Ninguno  
  
## <a name="permissions"></a>Permissions  
 Este procedimiento almacenado necesita el siguiente permiso:  
  
-   La pertenencia a la **ssis_admin** rol de base de datos.  
  
  
