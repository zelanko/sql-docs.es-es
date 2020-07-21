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
author: chugugrace
ms.author: chugu
ms.openlocfilehash: fdb3a128753ca5e6be23eadf1c0b4fb91e9654c4
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85674210"
---
# <a name="catalogstartup"></a>catalog.startup 

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

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
  
  
