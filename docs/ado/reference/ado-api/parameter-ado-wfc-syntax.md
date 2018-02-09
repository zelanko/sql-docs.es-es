---
title: "Parámetro (ADO - sintaxis WFC) | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 02/15/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
helpviewer_keywords:
- Parameter collection [ADO], ADO/WFC syntax
ms.assetid: d00d1e1e-14b1-41a2-a00f-2a3cb7396f15
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 05f3e2f6f6b3985c1c68604e6e9829c1b1f3eef1
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/09/2018
---
# <a name="parameter-ado---wfc-syntax"></a>Parámetro (ADO - sintaxis WFC)
## <a name="package-commswfcdata"></a>paquete com.ms.wfc.data  
  
### <a name="constructor"></a>Constructor  
  
```  
public Parameter()  
public Parameter(String name)  
public Parameter(String name, int type)  
public Parameter(String name, int type, int dir)  
public Parameter(String name, int type, int dir, int size)  
public Parameter(String name, int type, int dir, int size, Object value)  
```  
  
### <a name="methods"></a>Métodos  
  
```  
public void appendChunk(byte[] bytes)  
public void appendChunk(char[] chars)  
public void appendChunk(String chars)  
```  
  
### <a name="properties"></a>Propiedades  
  
```  
public int getAttributes()  
public void setAttributes(int attr)  
public int getDirection()  
public void setDirection(int dir)  
public String getName()  
public void setName(String name)  
public int getNumericScale()  
public void setNumericScale(int scale)  
public int getPrecision()  
public void setPrecision(int prec)  
public int getSize()  
public void setSize(int size)  
public int getType()  
public void setType(int type)  
public com.ms.com.Variant getValue()  
public void setValue(Object v)  
public AdoProperties getProperties()  
```  
  
## <a name="parameter-accessor-methods"></a>Métodos de descriptor de acceso de parámetro  
 El [valor](../../../ado/reference/ado-api/value-property-ado.md) propiedad de un [parámetro](../../../ado/reference/ado-api/parameter-object.md) objeto Obtiene o establece el contenido de ese objeto. El contenido se representa como una variante, un tipo de objeto que se puede asignar un valor y cualquiera de varios tipos de datos.  
  
 ADO/WFC implementa la **valor** propiedad con el **getValue** método, que devuelve un objeto VARIANT; y la **setValue** método, que toma una variante como argumento. Los tipos Variant son muy eficaces en algunos lenguajes, como Microsoft Visual Basic.  
  
 Además el **valor** propiedad ADO/WFC proporciona *descriptor de acceso* métodos que usan tipos de datos de Java para obtener y establecer el contenido de **parámetro** objetos. La mayoría de estos métodos tiene nombres de la forma **obtener *** DataType* o **establecer *** DataType*.  
  
 Hay una excepción notable: no hay ningún **getNull** propiedad; en su lugar, hay una **isNull** propiedad que devuelve un valor booleano que indica si el campo es null.  
  
```  
public boolean getBoolean()  
public void setBoolean(boolean v)  
public byte getByte()  
public void setByte(byte v)  
public double getDouble()  
public void setDouble(double v)  
public float getFloat()  
public void setFloat(float v)  
public int getInt()  
public void setInt(int v)  
public long getLong()  
public void setLong(long v)  
public short getShort()  
public void setShort(short v)  
public String getString()  
public void setString(String v)  
public boolean isNull()  
public void setNull()  
```  
  
## <a name="see-also"></a>Vea también  
 [Objeto Parameter](../../../ado/reference/ado-api/parameter-object.md)
