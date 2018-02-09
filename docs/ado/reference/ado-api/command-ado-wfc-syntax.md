---
title: Comando (ADO - sintaxis WFC) | Documentos de Microsoft
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
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
- Command collection [ADO], ADO/WFC syntax
ms.assetid: 39d0aa06-03ac-4c9a-8400-83947756ef99
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 310b7c246fc5d7006cc2e358340d0aa062dc3ab3
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/09/2018
---
# <a name="command-ado---wfc-syntax"></a>Comando (ADO - sintaxis WFC)
## <a name="package-commswfcdata"></a>paquete com.ms.wfc.data  
  
### <a name="constructor"></a>Constructor  
  
```  
public Command()  
public Command(String commandtext)  
```  
  
### <a name="methods"></a>Métodos  
  
```  
public void cancel()  
public com.ms.wfc.data.Parameter createParameter(String  
    Name, int Type, int Direction, int Size, Object Value)  
public Recordset execute()  
public Recordset execute(Object[] parameters)  
public Recordset execute(Object[] parameters, int options)  
public int executeUpdate(Object[] parameters)  
public int executeUpdate(Object[] parameters, int options)  
public int executeUpdate()  
```  
  
 El **executeUpdate** método es un caso especial de método que llama a ADO subyacente **ejecutar** método con determinados parámetros. El **executeUpdate** método no es compatible con la devolución de un **Recordset** objeto, por lo que la **ejecutar** del método *opciones* parámetro es modificar con **AdoEnums.ExecuteOptions.NORECORDS**. Después de la **ejecutar** método finaliza, su actualizada *RecordsAffected* parámetro se pasa a la **executeUpdate** método, que finalmente se devuelve como un **int**.  
  
### <a name="properties"></a>Propiedades  
  
```  
public com.ms.wfc.data.Connection getActiveConnection()  
public void setActiveConnection(com.ms.wfc.data.Connection con)  
public void setActiveConnection(String conString)  
public String getCommandText()  
public void setCommandText(String command)  
public int getCommandTimeout()  
public void setCommandTimeout(int timeout)  
public int getCommandType()  
public void setCommandType(int type)  
public String getName()  
public void setName(String name)  
public boolean getPrepared()  
public void setPrepared(boolean prepared)  
public int getState()  
public com.ms.wfc.data.Parameter getParameter(int n)  
public com.ms.wfc.data.Parameter getParameter(String n)  
public com.ms.wfc.data.Parameters getParameters()  
public AdoProperties getProperties()  
```  
  
## <a name="see-also"></a>Vea también  
 [Objeto Command (ADO)](../../../ado/reference/ado-api/command-object-ado.md)
