---
title: Ejemplo del método CreateRecordset (RDS) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- DataControl::CreateRecordset
- RDS.DataControl::CreateRecordset
- CreateRecordset
- RDSServer.DataFactory::CreateRecordset
- DataFactory::CreateRecordset
helpviewer_keywords:
- CreateRecordset method [RDS]
ms.assetid: 6840b1e5-c04d-4d3e-9dcc-42128c83492f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3c65f7d415864b169b683e0c9ab858506d31783b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67964515"
---
# <a name="createrecordset-method-rds"></a>Ejemplo del método CreateRecordset (RDS)
Crea una vacía, desconectado [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md).  
  
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, componentes de servidor RDS ya no están incluidos en el sistema operativo de Windows (consulte Windows 8 y [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obtener más detalles). Componentes de cliente RDS se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Deben migrar las aplicaciones que usan RDS a [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
object.CreateRecordset(ColumnInfos)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *Objeto*  
 Una variable de objeto que representa un [RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) o [RDS. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) objeto.  
  
 *ColumnsInfos*  
 Un **Variant** matriz de atributos que define cada columna en el **Recordset** creado. Cada definición de columna contiene una matriz de cuatro atributos necesarios y un atributo opcional.  
  
|Atributo|Descripción|  
|---------------|-----------------|  
|NOMBRE|Nombre del encabezado de columna.|  
|Type|Entero del tipo de datos.|  
|Tamaño|Entero del ancho en caracteres, independientemente del tipo de datos.|  
|Nulabilidad|Valor booleano.|  
|Escala (opcional)|Este atributo opcional define la escala para los campos numéricos. Si no se especifica este valor, se truncará a una escala de tres valores numéricos. No se ve afectada la precisión, pero el número de dígitos después del separador decimal se truncará a tres.|  
  
 El conjunto de matrices de columnas, a continuación, se agrupa en una matriz, que define el **Recordset**.  
  
## <a name="remarks"></a>Comentarios  
 Puede rellenar el objeto de negocios de servidor resultante **Recordset** con datos de un proveedor de datos que no sean OLE DB, como un sistema operativo archivo contenedor de cotizaciones.  
  
 La siguiente tabla se enumeran los [DataTypeEnum](../../../ado/reference/ado-api/datatypeenum.md) valores admitidos por el **CreateRecordset** método. El número que aparece es el número de referencia utilizado para definir los campos.  
  
 Cada uno de los tipos de datos es de longitud fija o longitud variable. Tipos de longitud fija deben definirse con un tamaño de -1, porque el tamaño es el predeterminado y sigue siendo necesaria una definición de tamaño. Tipos de datos de longitud variable permiten un tamaño de entre 1 y 32767.  
  
 Algunos de los tipos de datos de la variable, se puede convertir el tipo para el tipo indicado en la columna de sustitución. No verá las sustituciones hasta después de la **Recordset** está creado y rellenado. A continuación, puede comprobar el tipo de datos real, si es necesario.  
  
|Longitud|Constante|Number|Substitution|  
|------------|--------------|------------|------------------|  
|Corregido|**adTinyInt**|16||  
|Corregido|**adSmallInt**|2||  
|Corregido|**adInteger**|3||  
|Corregido|**adBigInt**|20||  
|Corregido|**adUnsignedTinyInt**|17||  
|Corregido|**adUnsignedSmallInt**|18||  
|Corregido|**adUnsignedInt**|19||  
|Corregido|**adUnsignedBigInt**|21||  
|Corregido|**adSingle**|4||  
|Corregido|**adDouble**|5||  
|Corregido|**adCurrency**|6||  
|Corregido|**adDecimal**|14||  
|Corregido|**adNumeric**|131||  
|Corregido|**adBoolean**|11||  
|Corregido|**adError**|10||  
|Corregido|**adGuid**|72||  
|Corregido|**adDate**|7||  
|Corregido|**adDBDate**|133||  
|Corregido|**adDBTime**|134||  
|Corregido|**adDBTimestamp**|135|7|  
|Variable|**adBSTR**|8|130|  
|Variable|**adChar**|129|200|  
|Variable|**adVarChar**|200||  
|Variable|**adLongVarChar**|201|200|  
|Variable|**adWChar**|130||  
|Variable|**adVarWChar**|202|130|  
|Variable|**adLongVarWChar**|203|130|  
|Variable|**adBinary**|128||  
|Variable|**adVarBinary**|204||  
|Variable|**adLongVarBinary**|205|204|  
  
## <a name="applies-to"></a>Se aplica a  
  
|||  
|-|-|  
|[Objeto DataControl (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)|[Objeto DataFactory (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)|  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo del método CreateRecordset (VB)](../../../ado/reference/ado-api/createrecordset-method-example-vb.md)   
 [Ejemplo del método CreateRecordset (VBScript)](../../../ado/reference/rds-api/createrecordset-method-example-vbscript.md)   
 [CreateObject (método) (RDS)](../../../ado/reference/rds-api/createobject-method-rds.md)



