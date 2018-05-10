---
title: catalog.check_schema_version | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: language-reference
ms.assetid: e0d5e9f5-59c6-4118-87b5-4aa5c37a7df6
caps.latest.revision: 5
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: cd5f2a54681bad2257ee16f266ae3e7008a23ce5
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="catalogcheckschemaversion"></a>catalog.check_schema_version
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Determina si el esquema del catálogo de SSISDB y los binarios de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] (ensamblado de ISServerExec y SQLCLR) son compatibles.  
  
 ISServerExec.exc registra un mensaje de error cuando el esquema y los archivos binarios son incompatibles.  
  
 La versión de esquema de SSISDB aumenta cuando el esquema se modifica durante la aplicación de revisiones y durante las actualizaciones. Se recomienda ejecutar este procedimiento almacenado después haber restaurado una copia de seguridad de SSISDB para asegurarse de que el esquema y los archivos binarios son compatibles.  
  
## <a name="syntax"></a>Sintaxis  
  
```sql  
catalog.check_schema_version [@use32bitruntime = ] use32bitruntime  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @use32bitruntime= ] *use32bitruntime*  
 Cuando el parámetro se establece en **Verdadero**, se llama a la versión de 32 bits dtexec. *use32bitruntime* es de tipo **Bool**.  
  
## <a name="result-set"></a>Conjunto de resultados  
 None  
  
## <a name="permissions"></a>Permisos  
 Este procedimiento almacenado necesita el siguiente permiso:  
  
-   Pertenencia al rol de base de datos de **ssis_admin**  
  
  
