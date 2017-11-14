---
title: "Consulta de método (RDS) | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
helpviewer_keywords:
- Query method [ADO]
ms.assetid: 20f2480f-3758-405d-a379-05a0dce74796
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 53647d80b2e6110e5af084e6a3f983381ced1690
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="query-method-rds"></a>Método Query (RDS)
Utiliza una cadena de consulta SQL válida para devolver un [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md).  
  
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, componentes de servidor RDS ya no están incluidos en el sistema operativo Windows (consulte Windows 8 y [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obtener más detalles). Componentes de cliente RDS se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Las aplicaciones que utilizan RDS deben migrar a [servicio de datos de WCF](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Set Recordset = DataFactory.Query(Connection, Query)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *Conjunto de registros*  
 Una variable de objeto que representa un **Recordset** objeto.  
  
 *Factory*  
 Una variable de objeto que representa un [RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) objeto.  
  
 *Conexión*  
 A **cadena** valor que contiene la información de conexión de servidor. Esto es similar a la [conectar](../../../ado/reference/rds-api/connect-property-rds.md) propiedad.  
  
 *Query*  
 A **cadena** que contiene la consulta SQL.  
  
## <a name="remarks"></a>Comentarios  
 La consulta debe usar el dialecto SQL del servidor de base de datos. Un estado de resultados se devuelve si se produce un error con la consulta que se ejecutó. El **consulta** método lleva a cabo no comprueba la sintaxis en el **consulta** cadena.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto DataFactory (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)  
  
## <a name="see-also"></a>Vea también  
 [Objeto DataFactory, método de consulta y ejemplo del método CreateObject (VBScript)](../../../ado/reference/rds-api/datafactory-object-query-method-and-createobject-method-example-vbscript.md)



