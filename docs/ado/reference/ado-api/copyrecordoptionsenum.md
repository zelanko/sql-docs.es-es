---
title: CopyRecordOptionsEnum | Documentos de Microsoft
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords: CopyRecordOptionsEnum
helpviewer_keywords: CopyRecordOptionsEnum enumeration [ADO]
ms.assetid: 2fa4eec5-d50b-4fd3-8ae7-40af441ba12b
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 018ebb888e190946ebac8e4b19b42302e430e3b0
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="copyrecordoptionsenum"></a>CopyRecordOptionsEnum
Especifica el comportamiento de la [CopyRecord](../../../ado/reference/ado-api/copyrecord-method-ado.md) método.  
  
|Constante|Valor|Description|  
|--------------|-----------|-----------------|  
|**adCopyAllowEmulation**|4|Indica que la *origen* proveedor intenta simular la copia mediante la descarga y operaciones de carga si se produce un error en este método debido a *destino*está en un servidor diferente o es atendido por otro proveedor que *origen*. Tenga en cuenta que las capacidades del proveedor que no son iguales pueden obstaculizar el rendimiento o perder datos.|  
|**adCopyNonRecursive**|2|Copia el directorio actual, pero ninguno de sus subdirectorios, en el destino. La operación de copia no es recursiva.|  
|**adCopyOverWrite**|1|Sobrescribe el archivo o directorio si el *destino* apunta a un archivo o directorio existente.|  
|**Como**|-1|Predeterminado: Realiza la operación de copia de forma predeterminada: la operación produce un error si el archivo de destino o el directorio ya existe y la operación copia de forma recursiva.|  
  
## <a name="adowfc-equivalent"></a>Equivalente ADO/WFC  
 Estas constantes no tienen equivalentes ADO/WFC.  
  
## <a name="applies-to"></a>Se aplica a  
 [Método CopyRecord (ADO)](../../../ado/reference/ado-api/copyrecord-method-ado.md)
