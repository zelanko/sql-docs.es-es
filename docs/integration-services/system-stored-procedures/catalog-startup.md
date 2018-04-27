---
title: catalog.startup | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: language-reference
ms.assetid: 271fd405-246a-4852-bfbe-f557241ce6ea
caps.latest.revision: 9
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0d2a407f0e45459dfeefa6265aceedce24e365a7
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2018
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
 None  
  
## <a name="permissions"></a>Permisos  
 Este procedimiento almacenado necesita uno de los permisos siguientes:  
  
-   Los permisos READ y MODIFY de la instancia de ejecución, los permisos READ y EXECUTE del proyecto y, si procede, los permisos READ del entorno al que se hace referencia  
  
-   Pertenencia al rol de base de datos de **ssis_admin**  
  
-   Pertenencia al rol de servidor de **sysadmin**  
  
  
