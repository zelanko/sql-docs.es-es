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
manager: craigg
ms.openlocfilehash: 4b376924dfb1833165a1f40ecfd1487c49eb2dcb
ms.sourcegitcommit: 63b4f62c13ccdc2c097570fe8ed07263b4dc4df0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/13/2018
ms.locfileid: "51604625"
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
  
|Attribute|Descripción|  
|---------------|-----------------|  
|Nombre|Nombre del encabezado de columna.|  
|Tipo|Entero del tipo de datos.|  
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
|Fixed|**adTinyInt**|16||  
|Fixed|**adSmallInt**|2||  
|Fixed|**son también tipos**|3||  
|Fixed|**adBigInt**|20||  
|Fixed|**adUnsignedTinyInt**|17||  
|Fixed|**adUnsignedSmallInt**|18||  
|Fixed|**adUnsignedInt**|19||  
|Fixed|**adUnsignedBigInt**|21||  
|Fixed|**adSingle**|4||  
|Fixed|**adDouble**|5||  
|Fixed|**adCurrency**|6||  
|Fixed|**adDecimal**|14||  
|Fixed|**adNumeric**|131||  
|Fixed|**adBoolean**|11||  
|Fixed|**adError**|10||  
|Fixed|**adGuid**|72||  
|Fixed|**adDate**|7||  
|Fixed|**adDBData**|133||  
|Fixed|**adDBTime**|134||  
|Fixed|**adDBTimestamp**|135|7|  
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



