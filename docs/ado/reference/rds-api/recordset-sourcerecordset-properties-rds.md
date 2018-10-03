---
title: Propiedades Recordset y SourceRecordset (RDS) | Microsoft Docs
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Recordset property [ADO]
ms.assetid: a29e3fb9-306d-497a-9a59-1856a914e5e9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bc0b548015cc63117cff566a2c4507b266d5ab7b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47657513"
---
# <a name="recordset-sourcerecordset-properties-rds"></a>Propiedades Recordset y SourceRecordset (RDS)
Indica el **Recordset** objeto devuelto desde un objeto de negocios personalizada.  
  
 **Se aplica a:** [objeto DataControl (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, componentes de servidor RDS ya no están incluidos en el sistema operativo de Windows (consulte Windows 8 y [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obtener más detalles). Componentes de cliente RDS se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Deben migrar las aplicaciones que usan RDS a [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
DataControl.SourceRecordset = Recordset  
Recordset = DataControl.Recordset   
```  
  
#### <a name="parameters"></a>Parámetros  
 *DataControl*  
 Una variable de objeto que representa un [RDS. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) objeto.  
  
 *Conjunto de registros*  
 Una variable de objeto que representa un **Recordset** objeto.  
  
## <a name="remarks"></a>Comentarios  
 Puede establecer el **SourceRecordset** propiedad a un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) devuelto desde un objeto de negocios personalizada.  
  
 Estas propiedades permiten que una aplicación controlar el proceso de enlace por medio de un proceso personalizado. Reciben un conjunto de filas que se encapsulan en un **Recordset** para que puedan interactuar directamente con el **Recordset**, realizar acciones como las propiedades de configuración o recorrer en iteración el **conjunto de registros** .  
  
 Puede establecer el **SourceRecordset** propiedad u obtenga el **Recordset** propiedad en tiempo de ejecución de código de secuencias de comandos.  
  
 **SourceRecordset** es una propiedad de solo escritura, en contraposición al **Recordset** propiedad, que es una propiedad de solo lectura.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto DataControl (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo de propiedades de SourceRecordset (VBScript) y conjunto de registros](../../../ado/reference/rds-api/recordset-and-sourcerecordset-properties-example-vbscript.md)   
 [Ejemplo del método CreateRecordset (RDS)](../../../ado/reference/rds-api/createrecordset-method-rds.md)   
 [Método Query (RDS)](../../../ado/reference/rds-api/query-method-rds.md)


