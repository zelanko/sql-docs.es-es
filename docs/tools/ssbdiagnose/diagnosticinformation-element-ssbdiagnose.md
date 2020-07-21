---
title: Elemento DiagnosticInformation
description: En SQL Server, el elemento DiagnosticInformation es el elemento raíz de un archivo de salida XML de ssbdiagnostic.
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: tools-other
ms.topic: conceptual
helpviewer_keywords:
- XML output file format [ssbdiagnose], diagnosticinformation element
- diagnosticinformation element
- ssbdiagnose
ms.assetid: 0cfda544-542c-4cf4-86d2-8031c91b10f6
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.openlocfilehash: d5e5e0b4e43a108b971b8982db91cb32b23e8e89
ms.sourcegitcommit: b8933ce09d0e631d1183a84d2c2ad3dfd0602180
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/13/2020
ms.locfileid: "83150587"
---
# <a name="diagnosticinformation-element-ssbdiagnose"></a>Elemento DiagnosticInformation (ssbdiagnose)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

El elemento **DiagnosticInformation** contiene todos los elementos que incluyen la información de diagnóstico generada por la utilidad. **DiagnosticInformation** es el elemento raíz de un archivo de salida XML **ssbdiagnostic** .  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
<DiagnosticInformation>   
    ...   
</DiagnosticInformation>  
```  
  
## <a name="element-attributes"></a>Atributos del elemento  
  
|Atributo|Descripción|  
|---------------|-----------------|  
|**None**|N/D|  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|**Tipo y longitud de los datos**|Ninguno.|  
|**Valor predeterminado**|Ninguno.|  
|**Repetición**|Una vez por archivo de salida XML **ssbdiagnose** .|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elementos|  
|------------------|--------------|  
|**Elemento primario**|Ninguno.|  
|**Elementos secundarios**|[Elemento Banner &#40;ssbdiagnose&#41;](../../tools/ssbdiagnose/banner-element-ssbdiagnose.md)<br /><br /> [Elemento Issue &#40;ssbdiagnose&#41;](../../tools/ssbdiagnose/issue-element-ssbdiagnose.md)|  
  
## <a name="remarks"></a>Observaciones  
 Para obtener más información acerca de los espacios de nombres XML, vea el artículo sobre [espacios de nombres en un documento XML](https://go.microsoft.com/fwlink/?LinkId=7341) en [!INCLUDE[msCoName](../../includes/msconame-md.md)] MSDN Library.  
  
## <a name="see-also"></a>Consulte también  
 [Utilidad ssbdiagnose &#40;Service Broker&#41;](../../tools/ssbdiagnose/ssbdiagnose-utility-service-broker.md)  
  
  
