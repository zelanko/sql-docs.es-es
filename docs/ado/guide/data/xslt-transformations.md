---
title: Transformaciones XSLT | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- XSLT transformations in ADO
ms.assetid: 1a46196e-839f-4734-a59e-2c64609ffb9e
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 1e443a2c131fc2338660c6ddfd0a09b285e1dba0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66699727"
---
# <a name="xslt-transformations"></a>Transformaciones XSLT
XSLT se puede aplicar al XML generado para transformarlos en otro formato. Conocer el formato XML en ADO ayuda a desarrollar plantillas XSLT que se pueden transformar en un formato más fácil de usar.  
  
 Por ejemplo, sabrá que cada fila del conjunto de registros se guarda como el elemento z: row dentro del elemento de datos: rs. De forma similar, cada campo del conjunto de registros se guarda como un par de atributo-valor para este elemento.  
  
## <a name="remarks"></a>Comentarios  
 El siguiente script XSLT se puede aplicar al XML que se muestra en la sección anterior, transformarlo en una tabla HTML que se mostrará en el explorador:  
  
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
  
 El XSLT convierte la secuencia XML generada por el método Save de ADO en una tabla HTML que muestra cada campo del conjunto de registros junto con un encabezado de tabla. Las filas y encabezados de tabla también se asignan colores y fuentes diferentes.  
  
## <a name="see-also"></a>Vea también  
 [Almacenar registros en formato XML](../../../ado/guide/data/persisting-records-in-xml-format.md)
