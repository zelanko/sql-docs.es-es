---
title: Elemento DTAXML (DTA) | Documentos de Microsoft
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
- DTAXML element
ms.assetid: 3d9942ed-8a27-40db-a7c9-808984d914a2
caps.latest.revision: 18
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: c521ec45d5b9227d53fcc9f39b59301ba18b7e69
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36111702"
---
# <a name="dtaxml-element-dta"></a>DTAXML (DTA, elemento)
  El elemento raíz de un archivo de entrada o salida XML del Asistente para la optimización de motor de base de datos, **DTAXML** , contiene todos los elementos que describen la entrada y la salida de optimización que genera el Asistente para la optimización de motor de base de datos.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
<DTAXML   
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"   
    xmlns="http://schemas.microsoft.com/sqlserver/2004/07/dta">  
    ...code removed here...  
</DTAXML>  
```  
  
## <a name="element-attributes"></a>Atributos del elemento  
  
|Attribute|Descripción|  
|---------------|-----------------|  
|`xmlns:xsi`|Requerido. Identifica el espacio de nombres de la instancia del esquema XML. Los atributos de este espacio de nombres se utilizan para hacer referencia al esquema usado para validar el archivo XML del Asistente para la optimización de motor de base de datos.<br /><br /> Valor requerido: [http://www.w3.org/2001/XMLSchema-instance](http://www.w3.org/2001/XMLSchema-instance)|  
|`xmlns`|Requerido. Identifica el espacio de nombres del Asistente para la optimización de motor de base de datos.<br /><br /> Si se modifica el archivo XML del Asistente para la optimización de motor de base de datos mediante el editor XML de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], este valor es utilizado por F1 Ayuda y la Ayuda dinámica para encontrar posibles temas de referencia en los Libros en pantalla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .<br /><br /> Valor requerido:<br /><br /> Espacio de nombres del[Esquema XML del Asistente para la optimización de motor de base de datos](http://go.microsoft.com/fwlink/?LinkId=43100) |  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|**Tipo y longitud de los datos**|Ninguno.|  
|**Valor predeterminado**|Ninguno.|  
|**Repetición**|Una obligatoria por archivo XML DTA|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elementos|  
|------------------|--------------|  
|**Elemento primario**|None|  
|**Elementos secundarios**|[Elemento DTAInput &#40;DTA&#41;](dtainput-element-dta.md)<br /><br /> `DTAOutput` Elemento (vea [esquema XML del Asistente de optimización de motor de base de datos](http://schemas.microsoft.com/sqlserver/) para obtener información)|  
  
## <a name="remarks"></a>Notas  
 Para obtener más información acerca de los espacios de nombres XML, vea el artículo sobre [espacios de nombres en un documento XML](http://go.microsoft.com/fwlink/?LinkId=7341) en [!INCLUDE[msCoName](../../includes/msconame-md.md)] MSDN Library.  
  
## <a name="example"></a>Ejemplo  
 Para ver ejemplos de elementos **DTAXML** típicos, consulte [Ejemplos de archivos de entrada XML &#40;DTA&#41;](xml-input-file-samples-dta.md).  
  
## <a name="see-also"></a>Vea también  
 [Referencia del archivo de entrada XML &#40;Asistente para la optimización de motor de base de datos&#41;](xml-input-file-reference-database-engine-tuning-advisor.md)   
 [Iniciar y utilizar el Asistente para la optimización de motor de base de datos](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md)  
  
  