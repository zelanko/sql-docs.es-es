---
title: catalog.check_schema_version | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: e0d5e9f5-59c6-4118-87b5-4aa5c37a7df6
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 23746065ca7096b0405114344d4f6a752bfedda1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68110466"
---
# <a name="catalogcheckschemaversion"></a>catalog.check_schema_version 

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


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
 Cuando el parámetro se establece en **1**, se llama a la versión de 32 bits de dtexec. *use32bitruntime* es de tipo **int**.  
  
## <a name="result-set"></a>Tipo de cursor  
 None  
  
## <a name="permissions"></a>Permisos  
 Este procedimiento almacenado necesita el siguiente permiso:  
  
-   Pertenencia al rol de base de datos de **ssis_admin**  
  
  
