---
title: catalog.create_execution_dump | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 91319b0b-5536-4ab4-a403-9559ed9dd177
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 72b833d5e11e5a034001eca4cac698b5ef392930
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68023511"
---
# <a name="catalogcreateexecutiondump"></a>catalog.create_execution_dump 

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Hace que un paquete en ejecución pause y cree un archivo de volcado. El archivo se almacena en la carpeta *\<unidad>* :\Archivos de programa\Microsoft SQL Server\130\Shared\ErrorDumps.  
  
## <a name="syntax"></a>Sintaxis  
  
```sql  
catalog.create_execution_dump [ @execution_id = ] execution_id  
  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @execution_id = ] *execution_id*  
 Identificador de ejecución del paquete en ejecución. El parámetro *execution_id* es de tipo **bigint**.  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente, se pide al paquete en ejecución con un identificador de ejecución 88 que cree un archivo de volcado.  
  
```sql
EXEC create_execution_dump @execution_id = 88  
```  
  
## <a name="return-codes"></a>Códigos de retorno  
 0 (correcto)  
  
 Cuando se produce un error en el procedimiento almacenado, se genera un error.  
  
## <a name="result-set"></a>Tipo de cursor  
 None  
  
## <a name="permissions"></a>Permisos  
 Este procedimiento almacenado necesita que los usuarios sean miembros del rol de base de datos **ssis_admin**.  
  
## <a name="errors-and-warnings"></a>Errores y advertencias  
 En la lista siguiente se describen las condiciones que hacen que el procedimiento almacenado genere un error.  
  
-   Se especifica un identificador de ejecución no válido.  
  
-   El paquete ya se ha completado.  
  
-   El paquete está creando actualmente un archivo de volcado.  
  
## <a name="see-also"></a>Consulte también  
 [Generar archivos de volcado para la ejecución de paquetes](../../integration-services/troubleshooting/generating-dump-files-for-package-execution.md)  
  
  
