---
title: EditModeEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- EditModeEnum
helpviewer_keywords:
- EditModeEnum enumeration [ADO]
ms.assetid: 45d54b6e-db2c-4553-9fd0-528147d6da2f
author: rothja
ms.author: jroth
ms.openlocfilehash: e4e16cbdddf39ba6abb03f93c35b2c2243d1bd71
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2020
ms.locfileid: "82765566"
---
# <a name="editmodeenum"></a>EditModeEnum
Especifica el estado de edición de un registro.  
  
|Constante|Valor|Descripción|  
|--------------|-----------|-----------------|  
|**adEditNone**|0|Indica que no hay ninguna operación de edición en curso.|  
|**adEditInProgress**|1|Indica que los datos del registro actual se han modificado pero no se han guardado.|  
|**adEditAdd**|2|Indica que se ha llamado al método [AddNew](../../../ado/reference/ado-api/addnew-method-ado.md) y que el registro actual del búfer de copia es un registro nuevo que no se ha guardado en la base de datos.|  
|**adEditDelete**|4|Indica que se ha eliminado el registro actual.|  
  
## <a name="adowfc-equivalent"></a>Equivalente de ADO/WFC  
 Paquete: **com. ms. wfc. Data**  
  
|Constante|  
|--------------|  
|AdoEnums. EditMode. NONE|  
|AdoEnums. EditMode. en curso|  
|AdoEnums. EditMode. ADD|  
|AdoEnums. EditMode. DELETE|  
  
## <a name="applies-to"></a>Se aplica a  
 [Propiedad EditMode](../../../ado/reference/ado-api/editmode-property.md)
