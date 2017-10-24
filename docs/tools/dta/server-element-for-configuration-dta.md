---
title: Elemento de servidor de Configuration (DTA) | Documentos de Microsoft
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- XML
helpviewer_keywords:
- Server element
ms.assetid: da9ff870-9cfd-42fe-994b-7b9292681f7d
caps.latest.revision: 13
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 548c08ab2bb5a12cade464305fa1ac0969c26bca
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="server-element-for-configuration-dta"></a>Server (DTA, elemento de Configuration)
  Contiene la información de identificación del servidor en el que quiere que el Asistente para la optimización de motor de base de datos evalúe la configuración hipotética (especificada por el elemento **Configuration** ).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
<Configuration>  
    <Server>  
...code removed here...  
    </Server>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|**Tipo y longitud de los datos**|Ninguno.|  
|**Valor predeterminado**|Ninguno.|  
|**Repetición**|Se requiere una vez por elemento **Configuration** .|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elementos|  
|------------------|--------------|  
|**Elemento primario**|[Elemento de configuración &#40; DTA &#41;](../../tools/dta/configuration-element-dta.md)|  
|**Elementos secundarios**|[Elemento de nombre de servidor &#40; DTA &#41;](../../tools/dta/name-element-for-server-dta.md)<br /><br /> [Elemento de la base de datos de configuración &#40; DTA &#41;](../../tools/dta/database-element-for-configuration-dta.md)|  
  
## <a name="remarks"></a>Comentarios  
 Solo es posible especificar un elemento **Server** para el elemento **Configuration** . Este elemento tiene el nombre **ServerTypecomplexType** en el [esquema XML del Asistente para la optimización de motor de base de datos](http://go.microsoft.com/fwlink/?linkid=43100). No confunda este elemento **Server** con el elemento secundario de **DTAInput** . Para obtener más información, vea [Server &#40;DTA, elemento&#41;](../../tools/dta/server-element-dta.md).  
  
## <a name="example"></a>Ejemplo  
 Para obtener un ejemplo de uso, vea [Ejemplo de archivo de entrada XML con configuración especificada por el usuario &#40;DTA&#41;](../../tools/dta/xml-input-file-sample-with-user-specified-configuration-dta.md).  
  
## <a name="see-also"></a>Vea también  
 [Referencia del archivo de entrada XML &#40;Asistente para la optimización de motor de base de datos&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  

