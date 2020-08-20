---
description: Propiedades avanzadas de conexión
title: Propiedades avanzadas de conexión | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 4edfab68-7e68-45e8-a3f3-a0049ff7eb9e
author: chugugrace
ms.author: chugu
ms.openlocfilehash: fd7ed8863356ff3e6b67d456628bd3dbc1ab6a5b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88484768"
---
# <a name="advanced-connection-properties"></a>Propiedades avanzadas de conexión

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Use el cuadro de diálogo **Propiedades avanzadas de conexión** para agregar más parámetros de conexión a la cadena de conexión.  
  
 Los parámetros de conexión adicionales pueden ser cualquier parámetro de conexión ODBC admitido por la instancia de base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que esté usando.  
  
 Los parámetros que se agregan mediante el cuadro de diálogo **Propiedades avanzadas de conexión** se agregan a los parámetros seleccionados en el cuadro de diálogo **Conectar con SQL Server** .  
  
 La última instancia de cada parámetro proporcionado invalida cualquier instancia anterior del mismo. Los parámetros que se agregan mediante el cuadro de diálogo **Parámetros de conexión adicionales** siguen y reemplazan a los parámetros proporcionados en el cuadro de diálogo **Conexión de SQL Server** . Por ejemplo, si en el cuadro de diálogo **Conexión de SQL Server** se especifica SERVER1 como el nombre del servidor y la página **Parámetros de conexión adicionales** contiene SERVER=SERVER2, la conexión se realizará con SERVER2.  
  
 Los parámetros que se agregan mediante el cuadro de diálogo **Propiedades avanzadas de conexión** se pasan como texto sin formato.  
  
> [!IMPORTANT]  
>  No incluya credenciales de inicio de sesión en el cuadro de diálogo **Propiedades avanzadas de conexión** . No se cifrarán cuando se pasen a través de la red.  
  
## <a name="see-also"></a>Consulte también  
 [Obtener acceso a la Consola del diseñador CDC](../../integration-services/change-data-capture/access-the-cdc-designer-console.md)   
 [Conexión de SQL Server para la creación de instancias](../../integration-services/change-data-capture/sql-server-connection-for-instance-creation.md)  
  
  
