---
title: Propiedades avanzadas de conexión | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 4edfab68-7e68-45e8-a3f3-a0049ff7eb9e
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 8cc86517a3a8ee3e7876c1c50b2db93512c61d50
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36201003"
---
# <a name="advanced-connection-properties"></a>Propiedades avanzadas de conexión
  Use el cuadro de diálogo **Propiedades avanzadas de conexión** para agregar más parámetros de conexión a la cadena de conexión.  
  
 Los parámetros de conexión adicionales pueden ser cualquier parámetro de conexión ODBC admitido por la instancia de base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que esté usando.  
  
 Los parámetros que se agregan mediante el cuadro de diálogo **Propiedades avanzadas de conexión** se agregan a los parámetros seleccionados en el cuadro de diálogo **Conectar con SQL Server** .  
  
 La última instancia de cada parámetro proporcionado invalida cualquier instancia anterior del mismo. Los parámetros que se agregan mediante el cuadro de diálogo **Parámetros de conexión adicionales** siguen y reemplazan a los parámetros proporcionados en el cuadro de diálogo **Conexión de SQL Server** . Por ejemplo, si en el cuadro de diálogo **Conexión de SQL Server** se especifica SERVER1 como el nombre del servidor y la página **Parámetros de conexión adicionales** contiene SERVER=SERVER2, la conexión se realizará con SERVER2.  
  
 Los parámetros que se agregan mediante el cuadro de diálogo **Propiedades avanzadas de conexión** se pasan como texto sin formato.  
  
> [!IMPORTANT]  
>  No incluya credenciales de inicio de sesión en el cuadro de diálogo **Propiedades avanzadas de conexión** . No se cifrarán cuando se pasen a través de la red.  
  
## <a name="see-also"></a>Vea también  
 [Obtener acceso a la consola del diseñador CDC](access-the-cdc-designer-console.md)   
 [Conexión de SQL Server para la creación de instancias](sql-server-connection-for-instance-creation.md)  
  
  