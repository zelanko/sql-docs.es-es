---
title: catalog.startup | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 271fd405-246a-4852-bfbe-f557241ce6ea
caps.latest.revision: "9"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b80919c3a754913ff15a5eed9ae37b39044977a0
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="catalogstartup"></a>catalog.startup
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Realiza el mantenimiento del estado de las operaciones del catálogo de SSISDB.  
  
 El procedimiento almacenado corrige el estado de los paquetes que estaban en ejecución si y cuando la instancia del servidor de [!INCLUDE[ssIS](../../includes/ssis-md.md)] se bloquea.  
  
 Tiene la posibilidad de habilitar el procedimiento almacenado para que se ejecute automáticamente cada vez que se reinicie la instancia del servidor de [!INCLUDE[ssIS](../../includes/ssis-md.md)]. Para ello, seleccione la opción **Habilitar la ejecución automática del procedimiento almacenado de Integration Services al iniciar SQL Server** en el cuadro de diálogo **Crear catálogo**.  
  
## <a name="syntax"></a>Sintaxis  
  
```sql  
catalog.startup  
```  
  
## <a name="return-code-value"></a>Valor de código de retorno  
 0 (correcto)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Ninguno  
  
## <a name="permissions"></a>Permissions  
 Este procedimiento almacenado necesita uno de los permisos siguientes:  
  
-   Los permisos READ y MODIFY de la instancia de ejecución, los permisos READ y EXECUTE del proyecto y, si procede, los permisos READ del entorno al que se hace referencia  
  
-   Pertenencia al rol de base de datos **ssis_admin**  
  
-   Pertenencia al rol de servidor **sysadmin**  
  
  
