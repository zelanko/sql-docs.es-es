---
title: Catalog.create_execution_dump | Documentos de Microsoft
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 91319b0b-5536-4ab4-a403-9559ed9dd177
caps.latest.revision: 12
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: b05e1b46845c0a2b5ee47b94dc239d79d4a12a17
ms.contentlocale: es-es
ms.lasthandoff: 09/26/2017

---
# <a name="catalogcreateexecutiondump"></a>catalog.create_execution_dump
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Hace que un paquete en ejecución pause y cree un archivo de volcado. El archivo se almacena en la  *\<unidad >*: carpeta \Program SQL Server\130\Shared\ErrorDumps.  
  
## <a name="syntax"></a>Sintaxis  
  
```sql  
catalog.create_execution_dump [ @execution_id = ] execution_id  
  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @execution_id =] *execution_id*  
 Identificador de ejecución del paquete en ejecución. El *execution_id* es **bigint**.  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente, se pide al paquete en ejecución con un identificador de ejecución 88 que cree un archivo de volcado.  
  
```sql
EXEC create_execution_dump @execution_id = 88  
```  
  
## <a name="return-codes"></a>Códigos de retorno  
 0 (correcto)  
  
 Cuando se produce un error en el procedimiento almacenado, se genera un error.  
  
## <a name="result-set"></a>Conjunto de resultados  
 Ninguno  
  
## <a name="permissions"></a>Permissions  
 Este procedimiento almacenado requiere que los usuarios sean miembros de la **ssis_admin** rol de base de datos.  
  
## <a name="errors-and-warnings"></a>Errores y advertencias  
 En la lista siguiente se describen las condiciones que hacen que el procedimiento almacenado genere un error.  
  
-   Se especifica un identificador de ejecución no válido.  
  
-   El paquete ya se ha completado.  
  
-   El paquete está creando actualmente un archivo de volcado.  
  
## <a name="see-also"></a>Vea también  
 [Generar archivos de volcado para la ejecución de paquetes](../../integration-services/troubleshooting/generating-dump-files-for-package-execution.md)  
  
  
