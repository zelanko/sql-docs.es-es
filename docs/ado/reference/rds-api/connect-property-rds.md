---
title: Propiedad Connect (RDS) | Documentos de Microsoft
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Connect property [ADO]
ms.assetid: dbad5e77-b213-4eb8-aecf-d60f203fdb59
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f30b087323ddfc26297844209d7293ea40ed5604
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="connect-property-rds"></a>Propiedad Connect (RDS)
Indica el nombre de base de datos desde el que se ejecutan las operaciones de consulta y actualización.  
  
 Puede establecer la **conectar** propiedad en tiempo de diseño en el [RDS. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) etiquetas de objeto del objeto, o en tiempo de ejecución de secuencias de comandos de código (por ejemplo, VBScript).  
  
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, componentes de servidor RDS ya no están incluidos en el sistema operativo Windows (consulte Windows 8 y [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obtener más detalles). Componentes de cliente RDS se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Las aplicaciones que utilizan RDS deben migrar a [servicio de datos de WCF](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Design time: <PARAM NAME="Connect" VALUE="ConnectionString">  
Run time: DataControl.Connect = "ConnectionString"  
```  
  
#### <a name="parameters"></a>Parámetros  
 *connectionString*  
 Una cadena de conexión válida. Para obtener más información acerca de las cadenas de conexión, consulte el [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md) propiedad o la documentación del proveedor.  
  
> [!NOTE]
>  Si especifica MS Remote como el proveedor para el **RDS. DataControl** crearía un escenario de cuatro niveles. Escenarios de más de tres niveles no se ha probado y no deberían ser necesario.  
  
 *DataControl*  
 Una variable de objeto que representa un **RDS. DataControl** objeto.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto DataControl (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo (VBScript) de la propiedad Connect](../../../ado/reference/rds-api/connect-property-example-vbscript.md)   
 [Método Query (RDS)](../../../ado/reference/rds-api/query-method-rds.md)   
 [Método Refresh (RDS)](../../../ado/reference/rds-api/refresh-method-rds.md)   
 [Método SubmitChanges (RDS)](../../../ado/reference/rds-api/submitchanges-method-rds.md)


