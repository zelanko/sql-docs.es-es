---
title: "SQL Server Compact Edition Connection Manager Editor (página todo) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.sqlmobileconnection.all.f1
helpviewer_keywords:
- SQL Server Compact Connection Manager Editor
ms.assetid: f9fbff4b-c502-44b3-8e7b-398d66e82206
caps.latest.revision: 26
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: c55d48a878bfee46c823303ce662baca0d34bfbd
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="sql-server-compact-edition-connection-manager-editor-all-page"></a>Editor del administrador de conexiones con SQL Server Compact Edition (página Todo)
  Use el cuadro de diálogo **Administrador de conexiones con SQL Server Compact Edition** para especificar las propiedades de conexiones a una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact.  
  
 Para obtener más información acerca del administrador de conexiones con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact Edition, vea [Administrador de conexiones con SQL Server Compact Edition](../../integration-services/connection-manager/sql-server-compact-edition-connection-manager.md).  
  
## <a name="options"></a>Opciones  
 **AutoShrink Threshold**  
 Especifique la cantidad de espacio disponible, como porcentaje, permitido en la base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact antes de que se ejecute el proceso de reducción automática.  
  
 **Extensión de bloqueo predeterminada**  
 Especifique el número de bloqueos de base de datos que adquiere la base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact antes de intentar concentrar los bloqueos.  
  
 **Default Lock Timeout**  
 Especifique el intervalo predeterminado, en milisegundos, que una transacción esperará un bloqueo.  
  
 **Flush Interval**  
 Especifique el intervalo, en segundos, transcurrido entre que las transacciones confirmadas vacían datos en el disco.  
  
 **Identificador de configuración regional**  
 Especifique el identificador de configuración regional (LCID) de la base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact.  
  
 **Max Buffer Size**  
 Especifique la cantidad máxima de memoria, en kilobytes, que usará [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact antes del vaciado de datos en el disco.  
  
 **Max Database Size**  
 Especifique el tamaño máximo, en megabytes, de la base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact.  
  
 **Modo**  
 Especifique el modo de archivo en el que se abrirá la base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact. El valor predeterminado para esta propiedad es **Lectura y escritura**.  
  
 La opción Modo tiene cuatro valores, tal como se describe en la siguiente tabla.  
  
|Value|Description|  
|-----------|-----------------|  
|**Solo lectura**|Especifica acceso de solo lectura a la base de datos.|  
|**Lectura y escritura**|Especifica permiso de lectura/escritura a la base de datos.|  
|**Exclusivo**|Especifica acceso exclusivo a la base de datos.|  
|**Shared Read**|Especifica que otros usuarios pueden leer de la base de datos al mismo tiempo.|  
  
 **Persist Security Info**  
 Especifique si la información de seguridad será devuelta como parte de la cadena de conexión. El valor predeterminado de esta opción es **False**.  
  
 **Temp File Directory**  
 Especifique la ubicación del archivo de base de datos temporal de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact.  
  
 **Origen de datos**  
 Especifique el nombre de la base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact.  
  
 **Contraseña**  
 Escriba la contraseña de la base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact.  
  
## <a name="see-also"></a>Vea también  
 [Referencia de mensajes y Error de Integration Services](../../integration-services/integration-services-error-and-message-reference.md)   
 [Editor del Administrador de SQL Server Compact Edition conexión &#40; Página de conexión &#41;](../../integration-services/connection-manager/sql-server-compact-edition-connection-manager-editor-connection-page.md)  
  
  
