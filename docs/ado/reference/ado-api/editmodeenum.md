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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0a8c4ddb27bbc6831095062af5491fb501b6d5b7
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "67933046"
---
# <a name="editmodeenum"></a>EditModeEnum
Especifica el estado de edición de un registro.  
  
|Constante|Value|Descripción|  
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
