---
title: catalog.startup | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 271fd405-246a-4852-bfbe-f557241ce6ea
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 3e5bec6c25f53da66a4f1d3e6aa09d94b621c81f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "65715872"
---
# <a name="catalogstartup"></a>catalog.startup 

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


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
  
  
