---
title: Procedimiento almacenado de validación (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 332d3c86-4440-4f12-a6cb-ffbfbccde52c
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: ddb720e7ec3196e1016e5737f2cb47e42f09ffbe
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/03/2018
ms.locfileid: "52799057"
---
# <a name="validation-stored-procedure-master-data-services"></a>Procedimiento almacenado de validación (Master Data Services)
  En [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], valide una versión para aplicar las reglas de negocios a todos los miembros de la versión del modelo.  
  
 En este tema se explica cómo usar el procedimiento almacenado **mdm.udpValidateModel** para validar datos. Si es administrador de la aplicación web [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] , puede realizar la validación en la interfaz de usuario en su lugar. Para obtener más información, consulte [Validar una versión con las reglas de negocios &#40;Master Data Services&#41;](validate-a-version-against-business-rules-master-data-services.md).  
  
> [!NOTE]  
>  Si invoca la validación antes de que se complete el proceso de almacenamiento provisional, no se validarán los miembros que no se hayan terminado de almacenar.  
  
## <a name="example"></a>Ejemplo  
  
```  
DECLARE @ModelName nVarchar(50) = 'Customer'   
DECLARE @Model_id int   
DECLARE @UserName nvarchar(50)= 'DOMAIN\user_name'   
DECLARE @User_ID int   
DECLARE @Version_ID int   
  
SET @User_ID = (SELECT ID    
                 FROM mdm.tblUser u   
                 WHERE u.UserName = @UserName)   
SET @Model_ID = (SELECT Top 1 Model_ID   
                 FROM mdm.viw_SYSTEM_SCHEMA_VERSION   
                 WHERE Model_Name = @ModelName)   
SET @Version_ID = (SELECT MAX(ID)   
                 FROM mdm.viw_SYSTEM_SCHEMA_VERSION   
                 WHERE Model_ID = @Model_ID)  
  
EXECUTE mdm.udpValidateModel @User_ID, @Model_ID, @Version_ID, 1  
  
```  
  
## <a name="parameters"></a>Parámetros  
 Los parámetros de este procedimiento son los siguientes:  
  
|Parámetro|Descripción|  
|---------------|-----------------|  
|UserID|Id. de usuario.|  
|Model_ID|Identificador del modelo.|  
|Version_ID|Identificador de versión.|  
  
## <a name="see-also"></a>Vea también  
 [Importación de datos &#40;Master Data Services&#41;](overview-importing-data-from-tables-master-data-services.md)   
 [Validar una versión con las reglas de negocios &#40;Master Data Services&#41;](validate-a-version-against-business-rules-master-data-services.md)  
  
  
