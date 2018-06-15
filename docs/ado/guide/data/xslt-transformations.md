---
title: Las transformaciones XSLT | Documentos de Microsoft
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- XSLT transformations in ADO
ms.assetid: 1a46196e-839f-4734-a59e-2c64609ffb9e
caps.latest.revision: 3
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 835362b473c16d71cbdd6c46d6e068a17d7d051d
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/11/2018
ms.locfileid: "35273474"
---
# <a name="xslt-transformations"></a>Transformaciones XSLT
XSLT se puede aplicar al XML generado para transformarlo en otro formato. Conocer el formato XML en ADO ayuda a crear plantillas XSLT que pueden transformarlo en un formulario más fácil de usar.  
  
 Por ejemplo, se sabe que cada fila del conjunto de registros se guarda como el elemento z: row dentro del elemento rs: data. De igual forma, cada campo del conjunto de registros se guarda como un par de atributo y valor para este elemento.  
  
## <a name="remarks"></a>Notas  
 La siguiente secuencia de comandos XSLT se puede aplicar en el XML mostrado en la sección anterior para transformar en una tabla HTML que se mostrará en el explorador:  
  
```  
<?xml version="1.0" encoding="ISO-8859-1"?>  
<html xmlns:xsl="http://www.w3.org/TR/WD-xsl">  
<body STYLE="font-family:Arial, helvetica, sans-serif; font-size:12pt; background-color:white">  
<table border="1" style="table-layout:fixed" width="600">  
  <col width="200"></col>  
  <tr bgcolor="teal">  
    <th><font color="white">CustomerId</font></th>  
    <th><font color="white">CompanyName</font></th>  
    <th><font color="white">ContactName</font></th>  
  </tr>  
<xsl:for-each select="xml/rs:data/z:row">  
  <tr bgcolor="navy">  
    <td><font color="white"><xsl:value-of select="@CustomerID"/></font></td>  
    <td><font color="white"><xsl:value-of select="@CompanyName"/></font></td>  
    <td><font color="white"><xsl:value-of select="@ContactName"/></font></td>   
  </tr>  
</xsl:for-each>  
</table>  
</body>  
</html>  
```  
  
 El XSLT convierte la secuencia XML generada por el método Save de ADO en una tabla HTML que muestra cada campo del conjunto de registros junto con un encabezado de tabla. Filas y encabezados de tabla también se asignan colores y fuentes diferentes.  
  
## <a name="see-also"></a>Vea también  
 [Almacenar registros en formato XML](../../../ado/guide/data/persisting-records-in-xml-format.md)
