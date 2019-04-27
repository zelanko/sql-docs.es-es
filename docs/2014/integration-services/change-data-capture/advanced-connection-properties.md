---
title: Propiedades avanzadas de conexión | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 4edfab68-7e68-45e8-a3f3-a0049ff7eb9e
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: a7a5744aa2adcaab74ca09bbb962c8c69d985b79
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62771521"
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
 [Obtener acceso a la Consola del diseñador CDC](access-the-cdc-designer-console.md)   
 [Conexión de SQL Server para la creación de instancias](sql-server-connection-for-instance-creation.md)  
  
  
