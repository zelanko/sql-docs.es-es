---
title: Elemento Server (DTA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- Server element
ms.assetid: 9fe0bfb4-3aa6-4eb2-a83e-c0d0e7d4e9f6
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f6c73db809e81cc9b6d1ee182227078a83688384
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/03/2018
ms.locfileid: "52767607"
---
# <a name="server-element-dta"></a>Server (DTA, elemento)
  Contiene la información de identificación del servidor en el que residen las bases de datos que se desean optimizar.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
<DTAInput>  
    <Server>  
    ...code removed here...  
    </Server>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|**Tipo y longitud de los datos**|Ninguno.|  
|**Valor predeterminado**|Ninguno.|  
|**Repetición**|Se requiere una vez por elemento `DTAInput`.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elementos|  
|------------------|--------------|  
|**Elemento primario**|[Elemento DTAInput &#40;DTA&#41;](dtainput-element-dta.md)|  
|**Elementos secundarios**|[Name &#40;DTA, elemento de Server&#41;](name-element-for-server-dta.md)<br /><br /> [Elemento Database para servidor &#40;DTA&#41;](database-element-for-server-dta.md)|  
  
## <a name="remarks"></a>Comentarios  
 Puede especificar solo uno `Server` (elemento) para el `DTAInput` elemento. Este elemento tiene el nombre **ServerDetailsTypecomplexType** en el esquema XML DTA. No confunda este elemento `Server` con el elemento secundario de `Configuration`. Para obtener más información, vea [Server &#40;DTA, elemento de Configuration&#41;](server-element-for-configuration-dta.md).  
  
## <a name="example"></a>Ejemplo  
 El ejemplo siguiente muestra cómo especificar la tabla **Sales.SalesPerson** en la base de datos de **AdventureWorks** en SERVER001:  
  
```xml  
<Server>  
  <Name>SERVER001</Name>  
  <Database>  
    <Name>AdventureWorks</Name>  
    <Schema>  
      <Name>Sales</Name>  
      <Table>  
        <Name>SalesPerson</Name>  
      </Table>  
    </Schema>  
  </Database>  
</Server  
```  
  
## <a name="see-also"></a>Vea también  
 [Referencia del archivo de entrada XML &#40;Asistente para la optimización de motor de base de datos&#41;](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
