---
title: DataTypeEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- DataTypeEnum
helpviewer_keywords:
- DataTypeEnum enumeration [ADO]
ms.assetid: 2c57eca6-9336-4b06-ba10-9fef5926b1d0
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 7cb3e56d0219973be97b694ee2b22dbbb58eb0d8
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/05/2019
ms.locfileid: "66698531"
---
# <a name="datatypeenum"></a>DataTypeEnum
Especifica el tipo de datos de un [campo](../../../ado/reference/ado-api/field-object.md), [parámetro](../../../ado/reference/ado-api/parameter-object.md), o [propiedad](../../../ado/reference/ado-api/property-object-ado.md). El indicador de tipo OLE DB correspondiente se muestra entre paréntesis en la columna de descripción de la tabla siguiente.  
  
|Constante|Valor|Descripción|  
|--------------|-----------|-----------------|  
|**AdArray**|0x2000|Un valor de marca, que siempre se combina con otra constante de tipo de datos, que indica una matriz de otro tipo de datos. No se aplica a ADOX.|  
|**adBigInt**|20|Indica un entero de ocho bytes con signo (DBTYPE_I8).|  
|**adBinary**|128|Indica un valor binario (DBTYPE_BYTES).|  
|**adBoolean**|11|Indica un **booleano** valor (DBTYPE_BOOL).|  
|**adBSTR**|8|Indica una cadena de caracteres terminada en null (Unicode) (DBTYPE_BSTR).|  
|**adChapter**|136|Indica un valor de capítulo de cuatro bytes que identifica las filas de un conjunto de filas secundario (DBTYPE_HCHAPTER).|  
|**adChar**|129|Indica un valor de cadena (DBTYPE_STR).|  
|**adCurrency**|6|Indica un valor de moneda (DBTYPE_CY). Moneda es un número de punto fijo con cuatro dígitos a la derecha del separador decimal. Se almacena en un entero con signo de ocho bytes escalado por 10.000.|  
|**adDate**|7|Indica un valor de fecha (DBTYPE_DATE). Una fecha se almacena como un valor double, la parte entera es el número de días transcurridos desde el 30 de diciembre de 1899 y la parte fraccionaria de los cuales es la fracción de un día.|  
|**adDBDate**|133|Indica un valor de fecha (aaaammdd) (DBTYPE_DBDATE).|  
|**adDBTime**|134|Indica un valor de hora (hhmmss) (DBTYPE_DBTIME).|  
|**adDBTimeStamp**|135|Indica una marca de fecha y hora (aaaammddhhmmss más una fracción de miles de millones) (DBTYPE_DBTIMESTAMP).|  
|**adDecimal**|14|Indica un valor numérico exacto con una precisión y escala fijas (DBTYPE_DECIMAL).|  
|**adDouble**|5|Indica un valor de punto flotante de precisión doble (DBTYPE_R8).|  
|**adEmpty**|0|No especifica ningún valor (DBTYPE_EMPTY).|  
|**adError**|10|Indica un código de error de 32 bits (DBTYPE_ERROR).|  
|**adFileTime**|64|Indica un valor de 64 bits que representa el número de intervalos de 100 nanosegundos desde el 1 de enero de 1601 (DBTYPE_FILETIME).|  
|**adGUID**|72|Indica un identificador único global (GUID) (DBTYPE_GUID).|  
|**adIDispatch**|9|Indica un puntero a un **IDispatch** interfaz en un objeto COM (DBTYPE_IDISPATCH).<br /><br /> **Tenga en cuenta** ADO no admite actualmente este tipo de datos. Uso puede provocar resultados imprevisibles.|  
|**adInteger**|3|Indica un entero de cuatro bytes con signo (DBTYPE_I4).|  
|**adIUnknown**|13|Indica un puntero a un **IUnknown** interfaz en un objeto COM (DBTYPE_IUNKNOWN).<br /><br /> **Tenga en cuenta** ADO no admite actualmente este tipo de datos. Uso puede provocar resultados imprevisibles.|  
|**adLongVarBinary**|205|Indica un valor binario long.|  
|**adLongVarChar**|201|Indica un valor de cadena larga.|  
|**adLongVarWChar**|203|Indica un valor de cadena Unicode terminada en null larga.|  
|**adNumeric**|131|Indica un valor numérico exacto con una precisión y escala fijas (DBTYPE_NUMERIC).|  
|**adPropVariant**|138|Indica una Automatización PROPVARIANT (DBTYPE_PROP_VARIANT).|  
|**adSingle**|4|Indica un valor de punto flotante de precisión sencilla (DBTYPE_R4).|  
|**adSmallInt**|2|Indica un entero de dos bytes con signo (DBTYPE_I2).|  
|**adTinyInt**|16|Indica un entero de un byte con signo (DBTYPE_I1).|  
|**adUnsignedBigInt**|21|Indica un entero de ocho bytes sin signo (DBTYPE_UI8).|  
|**adUnsignedInt**|19|Indica un entero de cuatro bytes sin signo (DBTYPE_UI4).|  
|**adUnsignedSmallInt**|18|Indica un entero de dos bytes sin signo (DBTYPE_UI2).|  
|**adUnsignedTinyInt**|17|Indica un entero de un byte sin signo (DBTYPE_UI1).|  
|**adUserDefined**|132|Indica una variable definida por el usuario (DBTYPE_UDT).|  
|**adVarBinary**|204|Indica un valor binario.|  
|**adVarChar**|200|Indica un valor de cadena.|  
|**adVariant**|12|Indica una automatización **Variant** (DBTYPE_VARIANT).<br /><br /> **Tenga en cuenta** ADO no admite actualmente este tipo de datos. Uso puede provocar resultados imprevisibles.|  
|**adVarNumeric**|139|Indica un valor numérico.|  
|**adVarWChar**|202|Indica una cadena de caracteres Unicode terminada en null.|  
|**adWChar**|130|Indica un caracteres de Unicode terminada en null, cadena (DBTYPE_WSTR).|  
  
## <a name="adowfc-equivalent"></a>Equivalente de ADO y WFC  
 Package: **com.ms.wfc.data**  
  
|Constante|  
|--------------|  
|AdoEnums.DataType.ARRAY|  
|AdoEnums.DataType.BIGINT|  
|AdoEnums.DataType.BINARY|  
|AdoEnums.DataType.BOOLEAN|  
|AdoEnums.DataType.BSTR|  
|AdoEnums.DataType.CHAPTER|  
|AdoEnums.DataType.CHAR|  
|AdoEnums.DataType.CURRENCY|  
|AdoEnums.DataType.DATE|  
|AdoEnums.DataType.DBDATE|  
|AdoEnums.DataType.DBTIME|  
|AdoEnums.DataType.DBTIMESTAMP|  
|AdoEnums.DataType.DECIMAL|  
|AdoEnums.DataType.DOUBLE|  
|AdoEnums.DataType.EMPTY|  
|AdoEnums.DataType.ERROR|  
|AdoEnums.DataType.FILETIME|  
|AdoEnums.DataType.GUID|  
|AdoEnums.DataType.IDISPATCH|  
|AdoEnums.DataType.INTEGER|  
|AdoEnums.DataType.IUNKNOWN|  
|AdoEnums.DataType.LONGVARBINARY|  
|AdoEnums.DataType.LONGVARCHAR|  
|AdoEnums.DataType.LONGVARWCHAR|  
|AdoEnums.DataType.NUMERIC|  
|AdoEnums.DataType.PROPVARIANT|  
|AdoEnums.DataType.SINGLE|  
|AdoEnums.DataType.SMALLINT|  
|AdoEnums.DataType.TINYINT|  
|AdoEnums.DataType.UNSIGNEDBIGINT|  
|AdoEnums.DataType.UNSIGNEDINT|  
|AdoEnums.DataType.UNSIGNEDSMALLINT|  
|AdoEnums.DataType.UNSIGNEDTINYINT|  
|AdoEnums.DataType.USERDEFINED|  
|AdoEnums.DataType.VARBINARY|  
|AdoEnums.DataType.VARCHAR|  
|AdoEnums.DataType.VARIANT|  
|AdoEnums.DataType.VARNUMERIC|  
|AdoEnums.DataType.VARWCHAR|  
|AdoEnums.DataType.WCHAR|  
  
## <a name="applies-to"></a>Se aplica a  
  
|||  
|-|-|  
|[Append (método) (ADO)](../../../ado/reference/ado-api/append-method-ado.md)|[Método CreateParameter (ADO)](../../../ado/reference/ado-api/createparameter-method-ado.md)|  
|[Ejemplo del método CreateRecordset (RDS)](../../../ado/reference/rds-api/createrecordset-method-rds.md)|[Tipo (propiedad, ADO)](../../../ado/reference/ado-api/type-property-ado.md)|
