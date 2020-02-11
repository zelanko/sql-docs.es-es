---
title: Propiedad Connect (RDS) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Connect property [ADO]
ms.assetid: dbad5e77-b213-4eb8-aecf-d60f203fdb59
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ba8b5aa1f59fbb161da878f5930f83d2f6ff0bdd
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "67964565"
---
# <a name="connect-property-rds"></a>Propiedad Connect (RDS)
Indica el nombre de la base de datos desde la que se ejecutan las operaciones de consulta y actualización.  
  
 Puede establecer la propiedad **Connect** en tiempo de diseño en [RDS. ](../../../ado/reference/rds-api/datacontrol-object-rds.md)Etiquetas de objeto del objeto DataControl, o en tiempo de ejecución en el código de scripting (por ejemplo, VBScript).  
  
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, los componentes de servidor RDS ya no se incluyen en el sistema operativo Windows (consulte la guía de compatibilidad de Windows 8 y [Windows server 2012](https://www.microsoft.com/download/details.aspx?id=27416) para obtener más detalles). Los componentes de cliente RDS se quitarán en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Las aplicaciones que utilizan RDS deben migrar al [servicio de datos de WCF](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Design time: <PARAM NAME="Connect" VALUE="ConnectionString">  
Run time: DataControl.Connect = "ConnectionString"  
```  
  
#### <a name="parameters"></a>Parámetros  
 *ConnectionString*  
 Cadena de conexión válida. Para obtener más información general sobre las cadenas de conexión, vea la documentación de [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md) o del proveedor.  
  
> [!NOTE]
>  Especificar MS Remote como proveedor para **RDS. DataControl** crearía un escenario de cuatro niveles. Los escenarios de más de tres niveles no se han probado y no deben ser necesarios.  
  
 *DataControl*  
 Variable de objeto que representa un objeto **RDS. Objeto DataControl** .  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto DataControl (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplo de la propiedad Connect (VBScript)](../../../ado/reference/rds-api/connect-property-example-vbscript.md)   
 [Query (método) (RDS)](../../../ado/reference/rds-api/query-method-rds.md)   
 [Método Refresh (RDS)](../../../ado/reference/rds-api/refresh-method-rds.md)   
 [Método SubmitChanges (RDS)](../../../ado/reference/rds-api/submitchanges-method-rds.md)


