---
title: Comando (ADO-sintaxis WFC) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Command collection [ADO], ADO/WFC syntax
ms.assetid: 39d0aa06-03ac-4c9a-8400-83947756ef99
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4722316cc92567000294c57089afd8840bea1bcd
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "67919827"
---
# <a name="command-ado---wfc-syntax"></a>Comando (ADO - sintaxis WFC)
## <a name="package-commswfcdata"></a>paquete com. ms. wfc. Data  
  
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
  
 El método **ExecuteUpdate** es un método especial de case que llama al método **Execute** de ADO subyacente con ciertos parámetros. El método **ExecuteUpdate** no admite la devolución de un objeto de **conjunto de registros** , por lo que el parámetro *Options* del método **Execute** se modifica con **AdoEnums. ExecuteOptions. NORECORDS**. Una vez completado el método **Execute** , el parámetro *RecordsAffected* actualizado se vuelve a pasar al método **ExecuteUpdate** , que finalmente se devuelve como un valor **int**.  
  
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
  
## <a name="see-also"></a>Consulte también  
 [Objeto Command (ADO)](../../../ado/reference/ado-api/command-object-ado.md)
