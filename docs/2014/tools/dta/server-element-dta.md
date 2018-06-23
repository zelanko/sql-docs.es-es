---
title: Elemento de servidor (DTA) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- XML
helpviewer_keywords:
- Server element
ms.assetid: 9fe0bfb4-3aa6-4eb2-a83e-c0d0e7d4e9f6
caps.latest.revision: 16
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 16bfbc4b45f8438ab5a4ab31cdce8183cb473e64
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36202637"
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
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|**Tipo y longitud de los datos**|Ninguno.|  
|**Valor predeterminado**|Ninguno.|  
|**Repetición**|Requiere una vez por `DTAInput` elemento.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elementos|  
|------------------|--------------|  
|**Elemento primario**|[Elemento DTAInput &#40;DTA&#41;](dtainput-element-dta.md)|  
|**Elementos secundarios**|[El nombre de elemento para el servidor &#40;DTA&#41;](name-element-for-server-dta.md)<br /><br /> [Elemento de la base de datos de servidor &#40;DTA&#41;](database-element-for-server-dta.md)|  
  
## <a name="remarks"></a>Notas  
 Puede especificar sólo una `Server` (elemento) para el `DTAInput` elemento. Este elemento tiene el nombre **ServerDetailsTypecomplexType** en el esquema XML DTA. No confunda este `Server` con el que es el elemento secundario del elemento el `Configuration` elemento. Para obtener más información, vea [Server &#40;DTA, elemento de Configuration&#41;](server-element-for-configuration-dta.md).  
  
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
  
  