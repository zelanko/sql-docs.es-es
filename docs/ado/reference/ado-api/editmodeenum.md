---
title: EditModeEnum | Documentos de Microsoft
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- EditModeEnum
helpviewer_keywords:
- EditModeEnum enumeration [ADO]
ms.assetid: 45d54b6e-db2c-4553-9fd0-528147d6da2f
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ba6822bfbb45ee547b87c56388b55d95195a7b63
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="editmodeenum"></a>EditModeEnum
Especifica el estado de edición de un registro.  
  
|Constante|Value|Description|  
|--------------|-----------|-----------------|  
|**adEditNone**|0|No indica que no hay ninguna operación de edición en curso.|  
|**adEditInProgress**|1|Indica que se ha modificado pero no se guardan los datos en el registro actual.|  
|**adEditAdd**|2|Indica que la [AddNew](../../../ado/reference/ado-api/addnew-method-ado.md) ha llamado al método y el registro actual en el búfer de copia es un nuevo registro que no se ha guardado en la base de datos.|  
|**adEditDelete**|4|Indica que se ha eliminado el registro actual.|  
  
## <a name="adowfc-equivalent"></a>Equivalente ADO/WFC  
 Paquete: **com.ms.wfc.data**  
  
|Constante|  
|--------------|  
|AdoEnums.EditMode.NONE|  
|AdoEnums.EditMode.INPROGRESS|  
|AdoEnums.EditMode.ADD|  
|AdoEnums.EditMode.DELETE|  
  
## <a name="applies-to"></a>Se aplica a  
 [Propiedad EditMode](../../../ado/reference/ado-api/editmode-property.md)
