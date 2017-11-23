---
title: "Ejemplo del método CreateRecordset (RDS) | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- DataControl::CreateRecordset
- RDS.DataControl::CreateRecordset
- CreateRecordset
- RDSServer.DataFactory::CreateRecordset
- DataFactory::CreateRecordset
helpviewer_keywords: CreateRecordset method [RDS]
ms.assetid: 6840b1e5-c04d-4d3e-9dcc-42128c83492f
caps.latest.revision: "17"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2a1bec5dc5b8c0e159755c9689aac0c9bfc40217
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="createrecordset-method-rds"></a>Ejemplo del método CreateRecordset (RDS)
Crea vacío, desconecta [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md).  
  
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, componentes de servidor RDS ya no están incluidos en el sistema operativo Windows (consulte Windows 8 y [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obtener más detalles). Componentes de cliente RDS se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Las aplicaciones que utilizan RDS deben migrar a [servicio de datos de WCF](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
object.CreateRecordset(ColumnInfos)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *Object*  
 Una variable de objeto que representa un [RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) o [RDS. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) objeto.  
  
 *ColumnsInfos*  
 A **Variant** matriz de atributos que define cada columna en el **Recordset** creado. Cada definición de columna contiene una matriz de cuatro atributos necesarios y un atributo opcional.  
  
|Attribute|Description|  
|---------------|-----------------|  
|Nombre|Nombre del encabezado de columna.|  
|Tipo|Entero del tipo de datos.|  
|Tamaño|Entero del ancho en caracteres, independientemente del tipo de datos.|  
|Nulabilidad|Valor booleano.|  
|Scale (opcional)|Este atributo opcional define la escala para los campos numéricos. Si no se especifica este valor, se truncará a una escala de tres valores numéricos. No se ve afectada la precisión, pero el número de dígitos después del separador decimal se truncará a tres.|  
  
 El conjunto de matrices de columnas, a continuación, se agrupa en una matriz, que define la **conjunto de registros**.  
  
## <a name="remarks"></a>Comentarios  
 El objeto empresarial de servidor puede rellenar resultante **Recordset** con datos de un proveedor de datos no OLE DB, como un sistema operativo archivos cotizaciones que lo contiene.  
  
 La siguiente tabla se recogen los [DataTypeEnum](../../../ado/reference/ado-api/datatypeenum.md) valores admitidos por el **CreateRecordset** método. El número que aparece es el número de referencia que se utiliza para definir campos.  
  
 Cada uno de los tipos de datos es de longitud fija o longitud variable. Tipos de longitud fija deben definirse con un tamaño de – 1, porque el tamaño es predeterminado y sigue siendo necesaria una definición de tamaño. Tipos de datos de longitud variable permiten un tamaño entre 1 y 32767.  
  
 En algunos de los tipos de datos de la variable, se puede convertir el tipo para el tipo indicado en la columna de sustitución. No verá las sustituciones hasta después de la **Recordset** se crea y se rellena. A continuación, puede comprobar el tipo de datos real, si es necesario.  
  
|Longitud|Constante|Number|Substitution|  
|------------|--------------|------------|------------------|  
|Fixed|**excepto adVarNumeric**|16||  
|Fixed|**adSmallInt**|2||  
|Fixed|**Tipos**|3||  
|Fixed|**adBigInt**|20||  
|Fixed|**adUnsignedTinyInt**|17||  
|Fixed|**adUnsignedSmallInt**|18||  
|Fixed|**adUnsignedInt**|19||  
|Fixed|**adUnsignedBigInt**|21||  
|Fixed|**adSingle**|4||  
|Fixed|**longitud fija**|5||  
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
|Variable|**Cada**|129|200|  
|Variable|**Parámetros**|200||  
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



