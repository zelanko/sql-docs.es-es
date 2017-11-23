---
title: Propiedad SQL | Documentos de Microsoft
ms.prod: sql-non-specified
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
helpviewer_keywords: SQL property [RDS]
ms.assetid: e0dabf23-a159-4fe5-a962-3df544a21f5c
caps.latest.revision: "16"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d1c6dfe09bf48ca48a9df29d066ef100403f7703
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="sql-property"></a>Propiedad SQL
Indica la cadena de consulta utilizada para recuperar la [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md).  
  
 Puede establecer la **SQL** propiedad en tiempo de diseño en el [RDS. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) etiquetas de objeto del objeto, o en tiempo de ejecución en código de scripting.  
  
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, componentes de servidor RDS ya no están incluidos en el sistema operativo Windows (consulte Windows 8 y [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obtener más detalles). Componentes de cliente RDS se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Las aplicaciones que utilizan RDS deben migrar a [servicio de datos de WCF](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Design time: <PARAM NAME="SQL" VALUE="QueryString">  
Run time: DataControl.SQL = "QueryString"  
```  
  
#### <a name="parameters"></a>Parámetros  
 *Cadena de consulta*  
 A **cadena** valor que contiene una solicitud de datos SQL válida.  
  
 *DataControl*  
 Una variable de objeto que representa un **RDS. DataControl** objeto.  
  
## <a name="remarks"></a>Comentarios  
 En general, esto es una instrucción SQL (mediante el dialecto del servidor de base de datos), como `"Select * from NewTitles"`. Para asegurarse de que los registros son coincidentes y actualizados con precisión, una consulta actualizable debe contener un campo que no sea un campo binario largo o un campo calculado.  
  
 El **SQL** propiedad es opcional si un objeto comercial personalizado de servidor recupera los datos para el cliente.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto DataControl (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo de la propiedad SQL (VBScript)](../../../ado/reference/rds-api/sql-property-example-vbscript.md)   
 [Propiedad Connect (RDS)](../../../ado/reference/rds-api/connect-property-rds.md)   
 [Método Query (RDS)](../../../ado/reference/rds-api/query-method-rds.md)   
 [Método Refresh (RDS)](../../../ado/reference/rds-api/refresh-method-rds.md)   
 [Método SubmitChanges (RDS)](../../../ado/reference/rds-api/submitchanges-method-rds.md)


