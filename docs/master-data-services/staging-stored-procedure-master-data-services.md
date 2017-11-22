---
title: Procedimiento almacenado de almacenamiento provisional (Master Data Services) | Microsoft Docs
ms.custom: 
ms.date: 04/01/2016
ms.prod: sql-non-specified
ms.prod_service: mds
ms.service: 
ms.component: master-data-services
ms.reviewer: 
ms.suite: sql
ms.technology: master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 6a613106-9f87-4caf-a23a-a726fc6561c5
caps.latest.revision: "15"
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5ca00f345569d60b7a7dcd78ce63fca380835feb
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="staging-stored-procedure-master-data-services"></a>Procedimiento almacenado de almacenamiento provisional (Master Data Services)
  Al iniciar el proceso de almacenamiento provisional desde [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], use uno de tres procedimientos almacenados.  
  
-   stg.udp_\<name>_Leaf  
  
-   stg.udp_\<name>_Consolidated  
  
-   stg.udp_\<name>_Relationship  
  
 Donde name es el nombre de la tabla de ensayo que se especificó cuando se creó la entidad.  
  
## <a name="staging-process-stored-procedure-parameters"></a>Parámetros de los procedimientos almacenados del proceso de almacenamiento provisional  
 En la tabla siguiente se enumeran los parámetros de estos procedimientos almacenados.  
  
|Parámetro|Description|  
|---------------|-----------------|  
|**VersionName**<br /><br /> Necesario|El nombre de la versión. Puede distinguir mayúsculas de minúsculas o no, según la configuración de intercalación de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .|  
|**LogFlag**<br /><br /> Necesario|Determina si se registran o no las transacciones durante el proceso de almacenamiento provisional. Los valores posibles son:<br /><br /> **0**: no registrar transacciones.<br /><br /> **1**: registrar transacciones.<br /><br /> <br /><br /> Para obtener más información sobre las transacciones, consulte [Transacciones &#40;Master Data Services&#41;](../master-data-services/transactions-master-data-services.md).|  
|**BatchTag**<br /><br /> Obligatorio, excepto para el servicio web|El valor de **BatchTag** como se especifica en la tabla de ensayo.|  
|**Batch_ID**<br /><br /> Solo lo necesita el servicio web|El valor de **Batch_ID** como se especifica en la tabla de almacenamiento provisional.|  
|**Nombre de usuario**|Parámetro opcional|  
|**Id. de usuario**|Parámetro opcional|  
  
### <a name="staging-process-stored-procedure-example"></a>Ejemplo de procedimiento almacenado del proceso de almacenamiento provisional  
 En el ejemplo siguiente se muestra cómo iniciar el proceso de almacenamiento provisional mediante el procedimiento almacenado de almacenamiento provisional.  
  
```  
USE [DATABASE_NAME]  
GO  
  
EXEC[stg].[udp_name_Leaf]  
      @VersionName = N'VERSION_1',  
@LogFlag = 1,  
@BatchTag = N'batch1'  
      @UserName=N’domain\user’  
  
GO  
  
```  
  
## <a name="see-also"></a>Vea también  
 [Procedimiento almacenado de validación &#40;Master Data Services&#41;](../master-data-services/validation-stored-procedure-master-data-services.md)   
 [Ver los errores que se producen durante el almacenamiento provisional &#40;Master Data Services&#41;](../master-data-services/view-errors-that-occur-during-staging-master-data-services.md)  
  
  
