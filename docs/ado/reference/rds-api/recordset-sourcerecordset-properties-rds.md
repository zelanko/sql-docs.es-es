---
title: Propiedades Recordset y SourceRecordset (RDS) | Documentos de Microsoft
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.prod: sql
ms.prod_service: drivers
ms.component: reference
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Recordset property [ADO]
ms.assetid: a29e3fb9-306d-497a-9a59-1856a914e5e9
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e934983f54be5644e945e4ecdcf201b793c33ea4
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="recordset-sourcerecordset-properties-rds"></a>Propiedades Recordset y SourceRecordset (RDS)
Indica el **Recordset** objeto devuelto desde un objeto comercial personalizado.  
  
 **Se aplica a:** [objeto DataControl (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, componentes de servidor RDS ya no están incluidos en el sistema operativo Windows (consulte Windows 8 y [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obtener más detalles). Componentes de cliente RDS se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Las aplicaciones que utilizan RDS deben migrar a [servicio de datos de WCF](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
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
 Puede establecer la **SourceRecordset** propiedad a una [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) devuelto desde un objeto de negocios personalizada.  
  
 Estas propiedades permiten que una aplicación controlar el proceso de enlace por medio de un proceso personalizado. Reciben un conjunto de filas que se encapsulan en un **Recordset** para que puedan interactuar directamente con el **Recordset**, realizar acciones como establecer propiedades o recorrer en iteración el **conjunto de registros** .  
  
 Puede establecer la **SourceRecordset** propiedad u obtenga el **Recordset** propiedad en tiempo de ejecución en código de scripting.  
  
 **SourceRecordset** es una propiedad de solo escritura, contrasta con la **Recordset** propiedad, que es una propiedad de solo lectura.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto DataControl (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo de propiedades de SourceRecordset (VBScript) y el conjunto de registros](../../../ado/reference/rds-api/recordset-and-sourcerecordset-properties-example-vbscript.md)   
 [Ejemplo del método CreateRecordset (RDS)](../../../ado/reference/rds-api/createrecordset-method-rds.md)   
 [Método Query (RDS)](../../../ado/reference/rds-api/query-method-rds.md)


