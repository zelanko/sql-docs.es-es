---
title: Propiedad SQL | Microsoft Docs
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- SQL property [RDS]
ms.assetid: e0dabf23-a159-4fe5-a962-3df544a21f5c
author: rothja
ms.author: jroth
ms.openlocfilehash: eb860ed19386b73d90fc26dab8fa96f4b9672a73
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2020
ms.locfileid: "82750729"
---
# <a name="sql-property"></a>Propiedad SQL
Indica la cadena de consulta utilizada para recuperar el [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md).  
  
 Puede establecer la propiedad **SQL** en tiempo de diseño en [RDS. ](../../../ado/reference/rds-api/datacontrol-object-rds.md)Etiquetas de objeto del objeto DataControl o en tiempo de ejecución en el código de scripting.  
  
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, los componentes de servidor RDS ya no se incluyen en el sistema operativo Windows (consulte la guía de compatibilidad de Windows 8 y [Windows server 2012](https://www.microsoft.com/download/details.aspx?id=27416) para obtener más detalles). Los componentes de cliente RDS se quitarán en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Las aplicaciones que utilizan RDS deben migrar al [servicio de datos de WCF](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Design time: <PARAM NAME="SQL" VALUE="QueryString">  
Run time: DataControl.SQL = "QueryString"  
```  
  
#### <a name="parameters"></a>Parámetros  
 *Cadenas*  
 Valor de **cadena** que contiene una solicitud de datos SQL válida.  
  
 *DataControl*  
 Variable de objeto que representa un objeto **RDS. Objeto DataControl** .  
  
## <a name="remarks"></a>Observaciones  
 En general, se trata de una instrucción SQL (con el dialecto del servidor de base de datos), como `"Select * from NewTitles"` . Para asegurarse de que los registros coinciden y se actualizan con precisión, una consulta actualizable debe contener un campo que no sea un campo binario largo o un campo calculado.  
  
 La propiedad **SQL** es opcional si un objeto empresarial personalizado del lado servidor recupera los datos para el cliente.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto DataControl (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplo de propiedad SQL (VBScript)](../../../ado/reference/rds-api/sql-property-example-vbscript.md)   
 [Propiedad Connect (RDS)](../../../ado/reference/rds-api/connect-property-rds.md)   
 [Query (método) (RDS)](../../../ado/reference/rds-api/query-method-rds.md)   
 [Método Refresh (RDS)](../../../ado/reference/rds-api/refresh-method-rds.md)   
 [Método SubmitChanges (RDS)](../../../ado/reference/rds-api/submitchanges-method-rds.md)


