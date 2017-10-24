---
title: Elemento DTAXML (DTA) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
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
- DTAXML element
ms.assetid: 3d9942ed-8a27-40db-a7c9-808984d914a2
caps.latest.revision: 18
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 175cfd247df19129f39d1e4ed8914da32dd57d11
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

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
  
|Atributo|Descripción|  
|---------------|-----------------|  
|**xmlns:xsi**|Requerido. Identifica el espacio de nombres de la instancia del esquema XML. Los atributos de este espacio de nombres se utilizan para hacer referencia al esquema usado para validar el archivo XML del Asistente para la optimización de motor de base de datos.<br /><br /> Valor requerido: [http://www.w3.org/2001/XMLSchema-instance](http://www.w3.org/2001/XMLSchema-instance)|  
|**xmlns**|Requerido. Identifica el espacio de nombres del Asistente para la optimización de motor de base de datos.<br /><br /> Si se modifica el archivo XML del Asistente para la optimización de motor de base de datos mediante el editor XML de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], este valor es utilizado por F1 Ayuda y la Ayuda dinámica para encontrar posibles temas de referencia en los Libros en pantalla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .<br /><br /> Valor requerido:<br /><br /> Espacio de nombres del[Esquema XML del Asistente para la optimización de motor de base de datos](http://go.microsoft.com/fwlink/?LinkId=43100) |  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|**Tipo y longitud de los datos**|Ninguno.|  
|**Valor predeterminado**|Ninguno.|  
|**Repetición**|Una obligatoria por archivo XML DTA|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elementos|  
|------------------|--------------|  
|**Elemento primario**|Ninguno|  
|**Elementos secundarios**|[DTAInput &#40;DTA, elemento&#41;](../../tools/dta/dtainput-element-dta.md)<br /><br /> Elemento**DTAOutput** (para obtener información, vea [Database Engine Tuning Advisor XML schema (Esquema XML del Asistente para la optimización de motor de base de datos)](http://schemas.microsoft.com/sqlserver/) ).|  
  
## <a name="remarks"></a>Comentarios  
 Para obtener más información acerca de los espacios de nombres XML, vea el artículo sobre [espacios de nombres en un documento XML](http://go.microsoft.com/fwlink/?LinkId=7341) en [!INCLUDE[msCoName](../../includes/msconame-md.md)] MSDN Library.  
  
## <a name="example"></a>Ejemplo  
 Para ver ejemplos de elementos **DTAXML** típicos, consulte [Ejemplos de archivos de entrada XML &#40;DTA&#41;](../../tools/dta/xml-input-file-samples-dta.md).  
  
## <a name="see-also"></a>Vea también  
 [Referencia del archivo de entrada XML &#40; motor de base de datos para la optimización Asistente &#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)   
 [Iniciar y utilizar el Asistente para la optimización de motor de base de datos](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md)  
  
  

